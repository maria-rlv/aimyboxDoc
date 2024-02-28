Core Android SDK provides the main Aimybox service that manages all nested processes of every voice assistant application (speech to text, NLU/NLP, text to speech and etc).

# When to use it

Use this component if you plan to embed voice assistant capabilities into your own Android application or device and would like to **implement assistant's UI/UX on your own**.

| If you have to quickly embed and customise a ready to use voice assistant UI into your Android application please use UI components library

# How to start using Aimybox Android SDK

The fastest way to start using Aimybox SDK for Android is to clone [ready to use Android assistant](https://github.com/just-ai/aimybox-android-assistant) and dive into the code. The following text highlight how to start using SDK from scratch.

Add the next dependencies Into your Android project's _build.gradle_ file

```
android {
  compileOptions {
    sourceCompatibility = JavaVersion.VERSION_1_8
    targetCompatibility = JavaVersion.VERSION_1_8
  }
}
    
repositories {
  maven("https://dl.bintray.com/aimybox/aimybox-android-sdk/")
}
    
dependencies {
  implementation("com.justai.aimybox:core:0.11.0")
}
```

|| Please use the [latest version of the Aimybox core library](https://bintray.com/aimybox/aimybox-android-sdk/core)

# Speechkit components

Every Aimybox powered voice assistant should use a speech to text and text to speech components to be able to recognise user's speech to the text and then synthesise the resulting text back to the user.

Aimybox provides a collection of ready to use speech to text and text to speech implementations.

|| You can also mix multiple speechkit libraries to use speech recognition technology from one vendor and text to speech from another one
| You can also implement and use any other speech to text or text to speech technology library through [SpeechToText](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/speechtotext/SpeechToText.kt) and [TextToSpeech](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/texttospeech/TextToSpeech.kt) interfaces

[Learn more about available speech to text components](/en/article/speech-to-text-components-1o8c1e5/)

# Wake word detector

The user has to activate your voice assistant before speaking with it. It could be a tap on the microphone button or any other way to wake the assistant.

One of the most popular way is to wake an assistant with special wake word like "Okay Google". In this case the voice assistant  listens for this word or phrase continuously in the background and once the user speaks it - the voice assistant starts to listen the voice command.

|| Please note that it's not mandatory to use wake word detector in your voice assistant

[Learn more about available voice trigger components](/en/article/voice-trigger-components-10r6m7z/)

# Aimybox instance

To start using voice features in your app you have to instantiate Aimybox service. For example, if you use Android speechkit it could look like this

```
val unitId = UUID.randomUUID().toString()
val textToSpeech = GooglePlatformTextToSpeech(context)
val speechToText = GooglePlatformSpeechToText(context)
val dialogApi = AimyboxDialogApi("your Aimybox project API key", unitId)
val aimybox = Aimybox(Config.create(speechToText, textToSpeech, dialogApi))
```

Further you can use `aimybox` in your application logic starting the speech recognition process through `startRecognition()` method. 

But before you have to **obtain a project API key** to make your assistant understand the user.

|| This step is mandatory only if you user Aimybox's NLU/NLP service to drive your voice assistant

### Project API key

Go to [Aimybox console](https://app.aimybox.com) and create a new project. Here you can add one or more voice skills to your assistant. Then click on **Train project** button and copy API key from the **project settings** screen.

The user can speak with some phrases that correspond to any enabled voice skills in your Aimybox console. The voice assistant sends the recognised user's speech to the Aimybox server and receives the result. If some meaningful intent was recognised, an assistant synthesises the result back to the user.

### Voice skills

There is a collection of ready to use voice skills in [Aimybox console](https://app.aimybox.com) and you can easily create your own voice skills for your assistant. Just click on **Create custom skill** button.

| Voice skills can perform some actions right on the device from where the user sent a voice command. To do this you have to add one or more [CustomSkill](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/CustomSkill.kt) implementations. [Learn more about custom skills](/en/article/android-custom-skills-1a1j0x0/)

[Learn more about voice skills](/en/article/voice-skills-overview-n49kfr/)

### Unit ID

The `unitId` variable contains a unique identifier of the device from where the user uses the voice assistant. **This value should be generated by your own** (in the example above it was generated randomly with `UUID` utility). 

|| It's important to have unique ID bound to the device because any dialog API manages the user's session based on some unique identifier. Otherwise different sessions may mix with each other at runtime.

### Dialog API

The NLU/NLP service recognises the user's intent, performs some actions and returns the result back to the voice assistant. Such a service could be online (works in the clouds) or offline (works right on the device).

Aimybox enables developers to connect their voice assistant to any NLU/NLP service, not only to the [Aimybox's one](https://app.aimybox.com). Thus you have to provide [DialogApi](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/api/DialogApi.kt) implementation during the `Aimybox` instantiation.

[Learn more about Dialog API](/en/article/dialog-api-components-1hm93q3/)

# More options and configuration update

`Aimybox` has to have a [configuration](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/Config.kt) that contains all it needs to work properly (like speech to text, text to speech and other features).

You can re-configure `Aimybox` instance on the fly through `updateConfiguration(config: Config)` method.

[Config](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/Config.kt) class contains everything you can configure in your `Aimybox`:

* **speechToText** - a [speech to text](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/speechtotext/SpeechToText.kt) service implementation that recognises the user's speech to the plain text

* **textToSpeech** - a [text to speech](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/texttospeech/TextToSpeech.kt) service implementation that synthesises the resulting speech to the user

* **voiceTrigger** - a [wake word detector](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/voicetrigger/VoiceTrigger.kt) implementation that detects the special wake phrase (like "Okay Google") invoking a speech to text service to recognise user's voice command (_this module is optional_)

* **dialogApi** - a [NLU/NLP](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/api/DialogApi.kt) service implementation that processes the recognised user's speech, performs some actions and returns meaningful response that can be visualised and synthesised back to the user

* **recognitionBehavior** - here you can configure the behaviour of wake word service (should it listen the wake word until the previous request is processed or not)

* **earcon** - a raw resource of special short sound that plays on speech recognition start (some speech to text implementations already have this one, thus this is _optional_)

* **skills** - a set [CustomSkill](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/CustomSkill.kt) that process the NLU/NLP results right on the device. [Learn more about custom skills](/en/article/android-custom-skills-1a1j0x0/)
