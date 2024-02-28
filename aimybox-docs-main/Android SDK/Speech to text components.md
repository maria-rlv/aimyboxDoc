Speech to text components enable a voice assistant to recognise user's speech and format it to the plain text. Then this text should be passed to another component named Dialog API to recognise a user's intention.

# Built-in speechkit libraries

Aimybox provides built-in speech to text components available via library dependencies:

* [Android speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/google-platform-speechkit) ${color}[#8c609e](**(supports offline mode)**)
* [Kaldi speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/kaldi-speechkit) ${color}[#8c609e](**(supports offline mode)**)
* [Pocketsphinx speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/pocketsphinx-speechkit) ${color}[#8c609e](**(supports offline mode)**)
* [Google Cloud speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/google-cloud-speechkit)
* [Houndify speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/houndify-speechkit)
* [Yandex Cloud speechkit](https://github.com/just-ai/aimybox-android-sdk/tree/master/yandex-speechkit)

# How to add another speech to text engine

You may wish to add another speech to text engine library for your assistant. To do this please implement [SpeechToText](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/speechtotext/SpeechToText.kt). You can see how it's done in any of built-in engines listed above.
