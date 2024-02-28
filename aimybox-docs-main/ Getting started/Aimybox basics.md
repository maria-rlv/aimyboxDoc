# What is Aimybox

Aimybox is an open source voice assistant that can be embedded into any application or device.

### Key features of Aimybox

* open source SDK for [Android](/en/article/android-sdk-overview-1ih4xn7/) and [iOS](/en/article/ios-sdk-overview-vwupih/)
* open source [embeddable voice assistant](https://github.com/just-ai/aimybox-android-assistant) with ready to use UI components
* [online platform](/en/article/introduction-to-aimybox-web-console-n49kfr/) for voice skills managing
* ready to use [speech to text](/en/article/speech-to-text-components-1o8c1e5/), [text to speech](/en/article/text-to-speech-components-btg1uk/), wake word detector and [NLU](/en/article/dialog-api-components-1hm93q3/) modules
* any developer could implement any other speech to text, text to speech and NLU engines

# How it works

![](/aimybox-scheme_191w70b.png)

The common flow of any voice assistant application or device looks like this:

1. The user activates the voice assistant app and speaks some command
2. The voice assistant recognises this speech to the text
3. Then it processes this text trying to recognise the user's intention
4. If there is something meaningful, the voice assistant performs appropriate actions
5. Then it synthesises the resulting speech and generates user interface with images, text, buttons and others UI components
6. The user hears the speech and decides to continue a dialog speaking the next phrase

_Aimybox handles all job regarding voice assistant functionality. It hides nested complexity of speech to text, NLP/NLU and text to speech processes managing, but enables developer to override any part of this logic._

| The main feature of Aimybox is extendable [architecture](/en/article/aimybox-architecture-17mr2q7/), thus there are no limitations for speech to text, text to speech and NLU/NLP - any developer could implement and use their own engine

Please [learn more about Aimybox architecture](/en/article/aimybox-architecture-17mr2q7/) to know how it works under the hood and how it's possible to implement Aimybox workflow for any platform you wish.

# Why it is better than Google Assistant

Aimybox is independent from any "global" speech to text, text to speech and NLU engines. It means that you can build your own voice user experience. There are no restrictions for voice skills functionality and content - thus your voice assistant can perform any logic and interact with user any way you wish.

Furthermore, Aimybox based voice assistant can perform any actions on device. This means that you can control any local services of the device, not only a cloud services when you create action for Google Assistant.

There are [much more restrictions](/en/article/other-assistants-restrictions-fjqu60/) of other global assistants you can avoid using Aimybox.

# How to start using Aimybox

The best way is to start from [Quick Start guide](/en/article/quick-start-s9rswy/). Then you can jump to our [Github repository](https://github.com/just-ai/aimybox-android-assistant) to checkout a complete voice assistant application and go through the code.
