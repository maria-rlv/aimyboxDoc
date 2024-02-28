In [Aimybox basics](/en/article/aimybox-basics-1aon9p9/) the main voice assistant's workflow was described. Here we provide a detailed technical description of how Aimybox core SDK is designed and how to implement this workflow for any other platform.

# Core SDK
![](/aimybox-core-1_qnlyft.png)
Here is a scheme of core components of Aimybox and it's dependencies.

* **Aimybox**. The core component that glues all other components together, dispatches invocations between them and provides public top-level methods to control state machine of the voice assistant.
* **SpeechToText**. An interface for speech recognition component. Uses microphone, recognises the user's speech and returns the recognised text. [Learn more](/en/article/speech-to-text-components-1o8c1e5/)
* **SpeechToTextComponent**. Holds an actual _SpeechToText_ implementation and manages it's lifecycle.
* **TextToSpeech**. An interface for speech synthesis component. Uses audio output and generates the speech from some text or SSML markup. [Learn more](/en/article/text-to-speech-components-btg1uk/)
* **TextToSpeechComponent**. Holds an actual _TextToSpeech_ implementation and manages it's lifecycle. It also parses SSML tags from the input text if any, separating a single text on a chunks of smaller texts and audio tracks. As well it may play non-text speeches like audio tracks if an actual TextToSpeech component cannot process such speeches..
* **VoiceTrigger**. An interface for hot word detector. Uses microphone and listens for some phrase continuously. As a rule works locally on device. Once the hot word is detected, Aimybox toggles the recognition process.
* **VoiceTriggerComponent**.  Holds an actual _VoiceTrigger_ implementation and manages it's lifecycle.
* **DialogApi**. An interface for NLU engine component. It receives the text to process and returns the recognised user's intent with additional metadata. As a rule works remotely. [Learn more](/en/article/dialog-api-components-1hm93q3/).
* **CustomSkill**. An interface for action component that performs some actions recognised in user's intent by _DialogApi_. There can be 0 or more custom skills that handle some of user's intents.
* **Config**. A component that holds all actual implementations of SpeechToText, TextToSpeech, VoiceTrigger and DialogApi. As well as some additional parameters of Aimybox. This configuration could be updated in runtime.

# Aimybox
Aimybox is a main component of SDK. It holds the configuration (**Config**) and manages the internal _state_ (**State**) of your voice assistant _lifecycle_.
The main purpose of Aimybox is to manage lifecycle and dispatch invocations to the _SpeechToText_, _TextToSpeech_, _VoiceTrigger_ and _DialogApi_ components. As well it provides some public methods that can be invoked from the top-level assistant application UI components.

Here is a [source code of Android Aimybox component](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/Aimybox.kt).

### Lifecycle
Aimybox guarantees that all components work properly together excepting race conditions, dead locks and resource leaks. That is why a special lifecycle was introduced based on simple state machine. Here is a list of this lifecycle states.
![](/aimybox-state-machine-1_uopnmp.png)

**STANDBY**
Voice assistant is ready to work. SpeechToText and TextToSpeech components are inactive. DialogApi component doesn't process any request. If VoiceTrigger component was configured, it's active and detects a hot word holding the microphone.

**LISTENING**
Voice assistant listens for the user's speech. VoiceTrigger and TextToSpeech are inactive. DialogApi component doesn't process any request. SpeechToText component holds the microphone and recognises the user's speech to text. User can cancel the recognition process to transit the Aimybox back to STANDBY state.

**PROCESSING**
Voice assistant recognises the intent from user's speech. All components excepting DialogApi are inactive. DialogApi makes some request to the NLU engine sending the recognised user's query. 
Once the intent was recognised, DialogApi looks for some CustomSkill that can handle this intent. If such a CustomSkill is found, it processes the intent. If the user closes an assistant's UI in this moment, this transits Aimybox back to STANDBY state.

**SPEAKING**
Voice assistant synthesises the output speech to the user. All components excepting TextToSpeech are inactive.TextToSpeech component holds audio output generating the speech from the intent's speeches list. It also can play some audio tracks one by one. Once synthesis is over, Aimybox transits back to STANDBY or LISTENING states depending on the DialogApi's response.

### Events
Aimybox allows top-level assistant's components (like UI) to subscribe to any events that are produced by low-level components. Each low-level component produces a list of events according to its' functionality.

# SpeechToText
This component is responsible for recognising the text from the user's speech in real time. As a rule it connects to some cloud based service sending the audio from the microphone chunk by chunk.

|| This component holds a microphone. Thus SpeechToText and VoiceTrigger components cannot work simultaneously.

Here is a [source code of Android SpeechToText component](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/speechtotext/SpeechToText.kt) and [some implementations](/en/article/speech-to-text-components-1o8c1e5/).

### SpeechToText events

* **RecognitionStarted**. Happens when SpeechToText actually starts the recognition.
* **RecognitionPartialResult**. Happens when SpeechToText has recognised the intermediate text from the chunk of speech.
* **RecognitionResult**. Happens when SpeechToText has recognised the final text from the speech.
* **EmptyRecognitionResult**. Happens when SpeechToText cannot recognise anything.
* **RecognitionCancelled**. Happens when user cancels the recognition.
* **SpeechStartDetected**. Happens when user starts to talk.
* **SpeechEndDetected**. Happens when user stops talking.
* **SoundVolumeRmsChanged**. Happens when sound volume of microphone input changes.

# VoiceTrigger
This component holds the microphone listening continuously for the hot word like "Okay Google" to activate the voice assistant. As a rule it uses some special libraries that perform all calculations locally on the device.

Here is a [source code of Android VoiceTrigger component](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/voicetrigger/VoiceTrigger.kt).

|| This component holds a microphone. Thus SpeechToText and VoiceTrigger components cannot work simultaneously.

### VoiceTrigger events

* **Started**. Happens when VoiceTrigger actually starts the hot word detection.
* **Stopped**.  Happens when VoiceTrigger stopped the hot word detection and released the microphone.
* **Triggered**. Happens when VoiceTrigger has detected the hot word.

# TextToSpeech
This component is responsible for synthesising the speech from the plain text. It receives a list of speeches and tries to synthesise each one by one.

Here is a [source code of Android TextToSpeech component](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/texttospeech/TextToSpeech.kt). 

### TextToSpeech events

* **SpeechSequenceStarted**. Happens when TextToSpeech actually starts to synthesise a list of speeches.
* **SpeechStarted**. Happens when TextToSpeech starts to synthesise the next speech from the list of speeches.
* **SpeechEnded**. Happens when TextToSpeech ends to synthesise the current speech.
* **SpeechSequenceCompleted**. Happens when TextToSpeech ends to synthesise the whole list of speeches.
* **SpeechSkipped**. Happens when TextToSpeech skips any of speeches (if it's empty for example).

# DialogApi
This component receives the text recognised by the SpeechToText and performs some action related to the user's intent. As a rule it connects with some cloud based NLU engine that recognises a language-independent intent from the text query. 

Each DialogApi implementation also provides a way to perform some intent related action locally on the device through CustomSkill components that could be added to the actual DialogApi component.

Here is a [source code of Android DialogApi component](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/api/DialogApi.kt).

### DialogApi events

* **RequestSent**. Happens when DialogApi has sent a request to the NLU engine.
* **ResponseReceived**. Happens when DialogApi has received a response from the NLU engine.
* **RequestCancelled**. Happens when a request to the NLU engine was canceled.

# CustomSkill
Once a response from the NLU engine was received, a DialogApi component looks up for the local CustomSkill implementation that can handle this response and perform some actions. This enables a voice assistant to communicate with local services of the device as well as local networks.

[Learn more about Android custom skills](/en/article/android-custom-skills-1a1j0x0/).

|| Note that only single CustomSkill can process a response from the DialogApi.
|| Note that CustomSkill receives an Aimybox reference as an argument and should manage it's state once all action have been performed by CustomSkill. As a rule a CustomSkill should call _standby_ method.

Here is a [source code of Android CustomSkill component](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/CustomSkill.kt).

### onRequest method
Each CustomSkill can add some additional metadata to the request object before a DialogApi will send it to the NLU engine. To do this each CustomSkill has onRequest method that is invoked by DialogApi right before the NLU engine requesting.

|| Note that DialogApi invokes onRequest for each configured CustomSkill thus every custom skill can add some piece of data to the request or modify it somewhere. But only one CustomSkill handles the response.
