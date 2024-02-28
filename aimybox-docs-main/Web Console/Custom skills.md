# Custom voice skills

You are not limited with only voice skills built-in into [Aimybox web console](/en/article/introduction-to-aimybox-web-console-n49kfr/). Custom skills enable you to create your own voice features for your voice assistant.

# How to create custom skill

Click on **Create custom skill** button in your voice project created through [Aimybox web console](/en/article/introduction-to-aimybox-web-console-n49kfr/). Here you have to setup some settings of your voice skill.

* **Skill name** - an arbitrary skill's name
* **Skill samples** - a collection of natural language phrases that activate your skill
* **Custom parameters** - if your skill uses some dynamic data like passwords or API keys you can configure it here
* **Skill source** - configure the place where your skill's logic is hosted

### Custom skill source

Your custom skill could be hosted anywhere in the cloud. Now you can use

* [Aimylogic](/en/article/aimylogic-webhook-5quhb1/)
* [Dialogflow](/en/article/dialogflow-agent-cqdvjn/) 
* [Custom Payload](/en/article/custom-payload-le1mvx/)

_Once the user speaks some phrase to the assistant, Aimybox recognises it and sends the recognised text to the Aimybox API. This phrase matches with sample phrases you've provided in your custom skills using the NLU algorithms. If any phrase matches to the skill successfully, Aimybox API picks this voice skill and it handles the user's query. Then all following user's queries go to this voice skill until the skill ends the session._
