# About this tutorial

In this tutorial you'll learn how to create a simple mobile voice assistant from scratch using [Aimybox Android SDK](/en/article/android-sdk-overview-1ih4xn7/) and [Aimylogic](/en/article/aimylogic-webhook-5quhb1/) chatbot builder.

### Rrequirements

This tutorial is aimed to _Android developers_ who are familiar with Android Studio and Java/Kotlin.
If you're not an Android developer, you nevertheless can learn how to create voice driven assistants using Aimybox.

### Source code

The complete code of this tutorial is available on [Github repository](https://github.com/just-ai/aimybox-android-tutorial). You can clone this project and run it on your device to see how it works.

# Step 1. Design voice app scenario.

First of all we have to create our voice app scenario. In other words - the _main logic of the voice assistant_ that will be built on the next steps.
Voice scenario includes some natural language driven dialogues that bring some value for the user.

| Aimybox enables you to create such a scenario with [any tool](/en/article/dialog-api-components-1hm93q3/) like Aimylogic, Dialogflow or Rasa. In this tutorial we'll use Aimylogic.

### Scenario

The scenario of our voice assistant will welcome the user  and ask them about their mood. A user can respond with phrases like _"I'm good"_ or _"I'm sad today"_.
If assistant detects that the user's mood is not good, it suggests them a funny cat photo (who doesn't like cats, is it?). The next short video shows how it could look like.

![](/ezgif-1-3d34e503f448_jcb20z.gif)

### Design scenario with Aimylogic

We will use [Aimylogic](https://aimylogic.com) as a tool for voice scenario building. It supports many APIs including different voice assistants like Google, Alexa and Aimybox.

1. Goto [www.aimylogic.com](https://aimylogic.com), register and create a new bot with **English language**.

2. Now it's blank canvas where we should add screens with blocks inside. Here is a full screencast of the process. 

${vimeo}[Aimybox Tutorial](385956467)

First of all we create a first screen with **Intent** block. Here we define phrases that user can speak once they launches our assistant. When user says "Hello" or "Hi there", an assistant should ask them about their mood. Click on the Hello intent and the second screen appears on the canvas.

Here we should add a Text block with assistant's prompt and question. The second block is an **Intent** again with possible user's answers like _"I'm good"_ or _"I'm sad today"_.

| Note that Aimylogic can understand phrases that are similar to the samples you've provided.

If the user is sad, our assistant should fetch and show some funny cat image. There is a great [JSON API](https://some-random-api.ml/img/cat) that returns a random cat's image on every GET HTTP request. It returns JSON with following format

```
{
  "link": "https://i.some-random-api.ml/NCgeBKe4og.jpg"
}
```

Thus we add a new screen with **HTTP Request** block inside. An URL should point to https://some-random-api.ml/img/cat. In Response tab we save the link field value from the response to the link variable this way - **$httpResponse.link**. On the next screen we can use this variable to show the image by URL with **Image** block.

Here we also add a question from the assistant ("Did this funny cat make your mood better?"), Intent block with possible intents like "Yes" and "No", and two buttons with "Yes" and "No" titles.
If user says "Yes" - the assistant should end the scenario with some final text (like "Great! See you latter!"). In the case of "No" response it should make an HTTP request again and show a new image.

3. Cool! It was really simple! Now we can save and test our scenario. Just click on **Test** button and go through a scenario.

4. Once it's tested successfully, we have to publish the scenario to the Aimybox channel. Click on the **Publish** button and then select **Aimybox** on the channels screen.
Click on "Get webhook" link to copy a webhook URL to your clipboard.

# 2. Step 2. Create Android application.

Okay, we have a working scenario published to the Aimybox channel. Now we have to connect our Android application to this endpoint through webhook URL.

### Create Android project

Goto the [Github repository](https://github.com/just-ai/aimybox-android-tutorial) and clone it to your computer. Now you have to import it to the Android Studio and change the existing webhook URL to your in the _AimyboxApplication_ class.

### Customize styles

[Aimybox SDK](/en/article/android-sdk-overview-1ih4xn7/) provides a ready to use [UI components](/en/article/android-ui-components-hvh9vw/) for fast prototyping and building of a voice enabled applications. You don't have to use it mandatory but it's useful to increase the speed of the voice apps development.

Of course this built-in UI components could be customised with custom styles in _styles.xml_ file. Here you can change the colours of the microphone button, it's position, background of the assistant and much more options.

### Run it

Once you're ready just build and run the project on your Android device connected to your computer. Tap on the microphone button to activate an assistant and say "Hello" to start a conversation.
You can see how Aimybox handles all nested job dispatching your request to the speech-to-text, Aimylogic and text-to-speech components.

### Exchange components

Aimybox contains a ready to use components for [speech-to-text](/en/article/speech-to-text-components-1o8c1e5/), [text-to-speech](/en/article/text-to-speech-components-btg1uk/) and [dialog-api](/en/article/dialog-api-components-1hm93q3/) engines, that can be used instead of standard Android's one. For example, you may wish to synthesise the text with some different voices or recognise speech through a different engine.

# Where to go next

You've done it! Now it's clear for you how it's easy to build voice driven assistants with Aimybox and Aimylogic.
For the next step it's great to dive into the [Aimybox SDK](/en/article/android-sdk-overview-1ih4xn7/) to learn more about how it works and how it can be embedded into any of your applications.
