The fallback feature of [Aimybox console](https://app.aimybox.com) enables your voice assistant to respond with predefined phrases on any unrecognised user's input.

# How to enable

In your project in [Aimybox console](https://app.aimybox.com) click on the **Fallback** menu.

![](/snimok-ekrana-2019-09-22-v-160_sua3hd.png)

Here you can add multiple phrases for the case if the user speaks something that doesn't correspond to any of enabled voice skills. Aimybox will pick one of these phrases randomly each time this case appears.

|| Please note that this feature is available only if your assistant uses Aimybox NLP service

# Context awareness

Fallback doesn't break the current context of Aimybox's built-in skills. Thus if some voice skill is on the foreground now and there is some conversation, the user may respond with something wrong, but fallback will not break the current conversation.

|| Note that this doesn't work for your custom skills because in this case the custom skill should implement it's own fallback feature.
