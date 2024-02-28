[UI components library](https://github.com/just-ai/aimybox-android-assistant) enables you to easily and very quickly embed ready to use voice assistant into your own Android application or create an all new voice assistant project.

This library contains all UI components and complete voice assistant UX implementation used by [Just AI](https://just-ai.com/) in many voice driven projects.

# When to use this library

If you need to embed and customise a voice assistant user interface into your application with screen.

# How to start using

There is a [Github repository](https://github.com/just-ai/aimybox-android-assistant) that describes the main steps of how to start using it.

| Also please checkout a [demo application](https://github.com/just-ai/aimybox-android-assistant/tree/master/app) that shows how it's easy to embed the voice assistant into your project

# The main concepts

The philosophy of Aimybox is going around the idea that _voice assistant can be easily embedded into any application_. The same way we can embed an online live chat widget on the website.

The voice assistant has some specific UX already known by the most of Android users (thanks to the global leaders like Google Assistant). And this UI/UX patterns should be represented in every voice assistant app to be accepted by users.

That's why we've simplified the voice assistant embedding process as much as possible! You have just [instantiate an Aimybox service](/en/article/core-android-sdk-2gs13n/) and add an [AimyboxAssistantFragment](https://github.com/just-ai/aimybox-android-assistant/blob/master/components/src/main/java/com/justai/aimybox/components/AimyboxAssistantFragment.kt) to your layout

```
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.layout_activity_main)

    supportFragmentManager.beginTransaction().apply {
        replace(R.id.assistant_container, AimyboxAssistantFragment())
        commit()
    }
}
```

That is all! If you run such a code you will find a small microphone button in the right bottom corner of the screen. The tap on it launches the assistant's UI that incapsulates all nested processes regarding speech recognition. NLP, UX and speech synthesis.

# UI customisation

You can customise the assistant's UI.

### Styles

If you need to change colours and some other attributes just override them in your _styles.xml_ file

```
<style name="AppTheme" parent="Theme.MaterialComponents.Light.NoActionBar">
        <item name="android:colorPrimary">@color/primary</item>
        <item name="android:colorPrimaryDark">@color/primaryDark</item>
        <item name="android:colorAccent">@color/accent</item>

        <item name="aimybox_assistantButtonTheme">@style/CustomAssistantButtonTheme</item>
        <item name="aimybox_recognitionTheme">@style/CustomRecognitionWidgetTheme</item>
        <item name="aimybox_responseTheme">@style/CustomResponseWidgetTheme</item>
        <item name="aimybox_imageReplyTheme">@style/CustomImageReplyWidgetTheme</item>
        <item name="aimybox_buttonReplyTheme">@style/CustomButtonReplyWidgetTheme</item>
    </style>

    <style name="CustomAssistantButtonTheme" parent="DefaultAssistantTheme.AssistantButton">
        <!-- <item name="aimybox_backgroundColor">@color/primary</item> -->
        <!-- <item name="aimybox_recordingAnimationColor">@color/recording</item> -->
        <!-- <item name="aimybox_buttonExpandedColor">@color/white</item> -->
    </style>

    <style name="CustomRecognitionWidgetTheme" parent="DefaultAssistantTheme.Widget.Recognition">
    </style>

    <style name="CustomResponseWidgetTheme" parent="DefaultAssistantTheme.Widget.Response">
    </style>

    <style name="CustomButtonReplyWidgetTheme" parent="DefaultAssistantTheme.Widget.ButtonReply">
    </style>

    <style name="CustomImageReplyWidgetTheme" parent="DefaultAssistantTheme.Widget.ImageReply">
    </style>
```

_Please refer to the corresponding parent theme to see which attributes you can customise in your style._

### Strings

Aimybox voice assistant UI shows the starting message when the user activates the assistant. This message could be customised through the **initial_phrase** string in _strings.xml_ file in your project.

```
<resources>
    <string name="initial_phrase">Hi! How can I help you?</string>
</resources>
```
