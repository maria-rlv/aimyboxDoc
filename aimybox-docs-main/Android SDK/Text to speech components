Text to speech component enables a voice assistant to synthesise the resulting speech back to the user once the NLU/NLP service has returned the result.

# Built-in text to speech libraries

Aimybox provides a ready to use text to speech libraries that can be used by your voice assistant through a dependencies

* [Android speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/google-platform-speechkit)
* [Google Cloud speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/google-cloud-speechkit)
* [Yandex Cloud speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/yandex-speechkit)

# How to use another text to speech engine

If you plan to use another text to speech engine you have to implement [TextToSpeech](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/texttospeech/TextToSpeech.kt). There are two types of text to speech engines: with [SSML](https://en.wikipedia.org/wiki/Speech_Synthesis_Markup_Language) support and without it.

If your custom text to speech engine doesn't support SSML out of the box, you have to implement [BaseTextToSpeech](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/texttospeech/BaseTextToSpeech.kt) instead.
