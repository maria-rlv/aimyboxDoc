# What is Aimylogic

[Aimylogic](https://aimylogic.com) provides a visual voice skills builder.

It can be used to create voice skills for your Aimybox powered project.

# How to use Aimylogic

* Just create a new Aimylogic bot and [enable Aimybox channel](https://help.aimylogic.com/docs/en/publication_channels/aimybox#how-to-connect-your-bot-to-a-device) in the settings. 

* Copy Aimybox webhook URL

* Paste this webhook URL into custom skill's webhook field

|| Please note that your Aimylogic bot scenario should contain at least one global Intents block with phrases that the user can pronounce

|| User has not to pronounce the same phrases strictly. Aimylogic's NLU can recognise the meaning of phrases and compare them with samples you've provided in your scenario using machine learning algorithms

# How to use Aimylogic without Aimybox console

You can use the same webhook URL obtained from Aimylogic in your assistant's initialisation block:

```
val dialogApi = AimyboxDialogApi("", unitId, "your Aimybox webhook URL goes here")
```
