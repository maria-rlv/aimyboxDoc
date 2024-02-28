# Aimybox Web console

If you plan to add _multiple_ voice skills into your assistant it's better to use [Aimybox web console](https://app.aimybox.com) that enables you to mix multiple voice skills **powered by different NLU engines** in the single voice project.

_Voice skill is a single piece of functionality of your voice assistant. It may be for example  a skill that searches articles on Wikipedia or weather forecast skill. Every skill has it's name, phrases that activate the skill and skill engine (see below)._

| The main purpose of Aimybox web console is to combine different voice skills into a single voice project and dispatch the user's requests between these skills.
# How does Aimybox console work

Aimybox project just combines different voice skills under the hood of your voice assistant's project. Once the user sends the voice request, Aimybox tries to match this request with one of enabled voice skills' activation phrases. If such a skill was found Aimybox routes this _and all subsequent requests_ to this skill until the skill returns _the end of session_ attribute. If there is no skill that can handle the request, Aimybox project will automatically respond with random phrases configured through [fallback feature](/en/article/fallback-1hpxmqx/).

# How to start using Aimybox web console

Just sign in to [Aimybox web console](https://app.aimybox.com) with your Github account and **create a new project** with one of supported language.

![](/wcpdmrpmoj_16ocq86_5tbl4i.gif)
|| Note that Aimybox console supports only a limited set of languages

### Skills marketplace

Aimybox web console provides a built-in collection of voice skills that can be added to your project. Just click on **Add** button on skills you would like to add to your project and then click on **Train project** on the top right corner.

|| Note that you have to re-train your project each time you add or remove voice skills

### Custom voice skills

You are not limited with only a built-in Aimybox's voice skills. Custom skills enable you to create your own voice features for your assistant.
Learn more about creating a custom skills [here](/en/article/custom-skills-c4iwy/).

# Project evaluating

To evaluate your project right in your browser just click on **Try in action** button and type some test requests in the popup window.

![](/ezgifcom-resize_9lb7lu.gif)

# Launching project

To start using your voice project in your voice assistant you have to copy **project's API key** from the project's settings and use it in the initialisation code of your mobile assistant that uses Aimybox SDK. [Learn more](/en/article/quick-start-s9rswy/) about how to do this.

# Direct NLU engine connection

You can develop a voice skill that implements [Aimybox HTTP API](/en/article/http-api-overview-1bpn7li/) and connect it directly to your `Aimybox` service in your application. In [Android](/en/article/android-sdk-overview-1ih4xn7/) and [iOS](/en/article/ios-sdk-overview-vwupih/) SDK you can pass the endpoint URL of your voice skill right in the [AimyboxDialogApi](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/api/aimybox/AimyboxDialogApi.kt) constructor.

Thus every user's request will go directly to the URL you've provided.

| For example you can develop a voice skill using [Aimylogic](/en/article/aimylogic-webhook-5quhb1/)

# Other NLU engines

If you don't want to use Aimybox Web console, you can connect your project directly to any other NLU engine you use. Here is a list of [currently supported engines](/en/article/dialog-api-components-1hm93q3/) you can use.

|| If there is a lack of the NLU engine you wish to use, you are always welcome to implement it and contribute to the [Github upstream repository](https://github.com/just-ai/aimybox-android-sdk)
