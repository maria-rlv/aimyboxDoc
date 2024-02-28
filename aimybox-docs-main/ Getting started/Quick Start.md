# What is Aimybox

Aimybox is an open source voice assistant that can be embedded into any mobile application. 
It includes ready to use [Android SDK](/en/article/core-android-sdk-2gs13n/), [iOS SDK](/en/article/ios-sdk-overview-vwupih/),  [HTTP API](/en/article/http-api-overview-1bpn7li/) and assistant UI components for both [Android](/en/article/android-ui-components-hvh9vw/) and [iOS](https://github.com/just-ai/aimybox-ios-assistant).

Aimybox doesn't implement any speech-to-text, text-to-speech or NLU engines. Instead, it provides a ready to use connectors to many of third-party modules like [Android Speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/google-platform-speechkit), [Kaldi](https://github.com/just-ai/aimybox-android-sdk/tree/master/kaldi-speechkit), [Pocketsphinx](https://github.com/just-ai/aimybox-android-sdk/tree/master/pocketsphinx-speechkit), [Google Cloud Speehkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/google-cloud-speechkit), [Aimylogic](/en/article/aimylogic-webhook-5quhb1/), [Dialogflow](https://github.com/just-ai/aimybox-android-sdk/tree/master/dialogflow-api), [Rasa AI](https://github.com/just-ai/aimybox-android-sdk/tree/master/rasa-api) and [others](https://github.com/just-ai/aimybox-android-sdk). Aimybox implements a [comprehensive voice assistant architecture](/en/article/aimybox-architecture-17mr2q7/) and glues all these components with each other in a proper way.

Thus every developer could pick some appropriate components for speech-to-text, text-to-speech and NLU, assemble an Aimybox instance and embed voice capabilities into their application with minimal effort.

### 😼 Simple tutorial

We recommend to start with our [simple tutorial](/en/article/aimybox-tutorial-1nsw2he/) to see how it's easy to build voice assistant using Aimybox and Aimylogic.

# How to start using Aimybox

All you need to embed a voice assistant into your Android application is to make the next simple steps.

### 1. Clone Aimybox sample app

The easiest way to try Aimybox - is to **clone ready to use Android application** from [Aimybox Github repository](https://github.com/just-ai/aimybox-android-assistant).

|| You have to use some Android IDE to build your app like [Android Studio](https://developer.android.com/studio)

![](/snimok-ekrana-2019-08-16-v-183_19whbgk.png)

Then you have just connect any Android device to your PC via USB and click on green play button to build and deploy your voice assistant.
A new Android will be launched on your device and you can just tap on the microphone button and say something to see how your assistant reacts.

### 2. Create your own voice poject

All you need to do next - is to select an appropriate [NLU engine](/en/article/dialog-api-components-1hm93q3/) and create the voice skills using it. Please refer to the documentation of selected NLU to learn how to create a voice skill.

To mix multiple voice skills in the single voice project you can use [Aimybox Web console](/en/article/introduction-to-aimybox-web-console-n49kfr/). It also contains a marketplace of ready to use voice skills, so it may be the easiest way to start using Aimybox.

### 3. Connect voice project to the app

Once you've created a voice project (using Aimybox Web console or directly on the favourite NLU engine) you have to connect it with your Aimybox powered application. 

|| If you don't use Aimybox Web console please refer to the selected [NLU engine](/en/article/dialog-api-components-1hm93q3/) module manual to connect it to your app

_For example, if you use [Aimybox Web console](/en/article/introduction-to-aimybox-web-console-n49kfr/), you have to create an Aimybox channel, copy your Aimybox project's API key and paste it into the Aimybox initialisation block

```
val dialogApi = AimyboxDialogApi("API key goes here", unitId)
```

### 4. Start your app

Start your application on the device. You will see how Aimybox SDK handles all job regarding speech recognition, speech synthesis and NLU. It also provides a ready to use UI that can be fully customised or replaced with your own.

# Where to go next

Learn more about how to use Aimybox in [Aimybox basics](/en/article/aimybox-basics-1aon9p9/). If you would like to deep into the architecture to implement your own component, please [read this article](/en/article/aimybox-architecture-17mr2q7/).
