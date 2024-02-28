_Custom skills_ is a great feature of Aimybox that enables the voice assistant to perform any actions right on the device from where the user speaks their voice commands.

|| Google Assistant Actions or Amazon Alexa skills don't provide such ability because the voice action or skill works entirely in the cloud and doesn't have an access to the local device's services

_For example, a custom skill could launch some activity or perform some actions in the user's local network._

# How to create a custom skill

To create a new custom skill you have to implement a [CustomSkill](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/CustomSkill.kt) interface. Then you have to add your custom skill implementation in the [Config](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/core/Config.kt) of your `Aimybox` instance.

# Custom skill lifecycle

The custom skill has the following lifecycle methods that are called by Aimybox service

### canHandleRequest

This method should return `true` if your custom skill can handle a particular [Request](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/model/Request.kt) from the dialog API.

### onRequest

This method will be called by Aimybox service right after the user's speech was recognised. Custom skill can add some additional data to the [Request](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/model/Request.kt) that will be sent to the configured dialog API then.

_For example, your custom skill can add the current user's geolocation to help your weather forecast service find the right data._

### canHandle

This method should return `true` if your custom skill can handle a particular [Response](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/model/Response.kt) from the dialog API.

| As a rule custom skill looks only on the `action` field of `Response` object to determine if it can handle this particular response
|| If Aimybox service didn't find any custom skill that can handle this response, it just executes the default action - synthesises the speech from this response and continue speech recognition if needed

### onResponse

The main method of the custom skill that should perform the actual action for the particular dialog API's [Response](https://github.com/just-ai/aimybox-android-sdk/blob/master/core/src/main/java/com/justai/aimybox/model/Response.kt)).

An `Aimybox` instance also passed to this method because custom skill should manage the state of `Aimybox` in the case it can handle this response. It means that your custom skill should synthesise the speech through `speak()` method or just call `standby()` method right after processing.

|| Note that you have to call `standby()` method if your custom skill doesn't synthesise anything back to the user

This method also receives a `callDefaultHandler` as an argument. This function can be called if you won't synthesise a response on your own and would like to invoke a default Aimybox's implementation.

# Example

Here is a simple example of such custom skill that performs some logic on the device

```
class MyCustomSkill: CustomSkill<AimyboxRequest, AimyboxResponse> {

     var handleRequest = true 

    override fun canHandleRequest(request: AimyboxRequest)  = handleRequest

    override fun canHandle(response: AimyboxResponse) = response.action == "my_action"

    override suspend fun onRequest(request: AimyboxRequest): AimyboxRequest {
        request.data?.addProperty("my_string_property", "some string")
        request.data?.addProperty("my_number_property", 10)
        return request
    }

    override suspend fun onResponse(
        response: AimyboxResponse,
        aimybox: Aimybox,
        defaultHandler: suspend (Response) -> Unit
    ) {
        // perform some local action here
        aimybox.standby()
    }
}
```

Then such a skill should be added to the Dialog API implementation (`AimyboxDialogApi` in our case)

```
val dialogApi = AimyboxDialogApi(
    AIMYBOX_API_KEY, unitId, 
    customSkills = linkedSetOf(MyCustomSkill())
)
```

You can get access to a skill by its class name via `DialogApi`  method `getCustomSkill()`

```
val customSkill = aimybox.config.dialogApi.getCustomSkill("MyCustomSkill")

```

|| Please note that every custom skill could be added only to the corresponding DialogAPI implementation because `Request` and `Response` are different for every DialogAPI
