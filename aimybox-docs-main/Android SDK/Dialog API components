Dialog API component enables your voice assistant to recognise the user's speech intention, perform some useful actions and return the meaningful response back to the user that can be synthesised by [text to speech component](/en/article/text-to-speech-components-btg1uk/).

# Built-in dialog API libraries

Aimybox provides these ready to use NLU engine implementations:

* [Aimybox API](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/api/aimybox/AimyboxDialogApi.kt) - processes each user's query through the [Aimybox console API](/en/article/introduction-to-aimybox-web-console-n49kfr/) or direct webhook that implements [Aimybox HTTP API](/en/article/http-api-overview-1bpn7li/) (for example [Aimylogic webhook](/en/article/aimylogic-webhook-5quhb1/))

* [Dialogflow](https://github.com/just-ai/aimybox-android-sdk/tree/master/dialogflow-api) - ready to use connector for [Google Dialogflow agent](https://dialogflow.com)

* [Rasa AI](https://github.com/just-ai/aimybox-android-sdk/tree/master/rasa-api) - ready to use connector for [Rasa AI](https://rasa.ai)

| Aimybox Web console service combines multiple voice skills driven by different NLU engines under the hood. [Learn more](/en/article/introduction-to-aimybox-web-console-n49kfr/)

# How to implement another NLU engine API

You can use another NLU engine in your voice assistant. Just implement [DialogAPI](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/api/DialogApi.kt) interface and configure it when instantiate `Aimybox`.
