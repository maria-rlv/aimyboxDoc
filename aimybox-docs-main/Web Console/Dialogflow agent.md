# What is Dialogflow

[Dialogflow](https://dialogflow.com) is a conversation platform created by Google.

It can be used to create custom voice skills for your Aimybox project and connect it to your voice assistant.

# How to use Dialogflow

Just follow [Dialogflow tutorials](https://dialogflow.com/docs/tutorial-build-an-agent) to create new agent. Then go through the next steps to connect it to your Aimybox project:

* [obtain service account](https://dialogflow.com/docs/reference/v2-auth-setup) for your Dialogflow agent

* open downloaded JSON file and copy it's content

* go to [Aimybox console](https://app.aimybox.com) and create a **new custom skill**

* select **Dialogflow agent** as a source of your custom skill and paste service account JSON content

|| Please note that your Dialogflow agent should contain intents with the same sample phrases as your Aimybox custom skill

|| Your Dialogflow agent should contain at least one intent that end the session

# How to use Dialogflow without Aimybox console

If you need to use Dialogflow agent as a primary voice skill in your assistant and don't need to mix it wit other skills, you can use [Dialogflow module](https://github.com/just-ai/aimybox-android-sdk/tree/master/dialogflow-api) directly instead of connecting to Aimybox API.
