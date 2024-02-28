# Custom Payload

With custom payload you can create a custom skill that only returns a static response or responses array.

In this case you don't have to create any skill's logic using any tools like Aimylogic or Dialogflow. All you need - is to define the JSON payload that will be returned to your voice assistant.

# How to use

You have to define payload JSON that contains a reply or an array of replies in the format of [Aimybox HTTP API](/en/article/http-api-overview-1bpn7li/). For example

```
{
  "type": "text",
  "text": "There is some custom text"
}
```

If you need to send multiple replies you ca define JSON array

```
[
  {
    "type": "image",
    "imageUrl": "https://somaddress.com/image.jpg"
  },
  {
    "type": "text",
    "text": "Some text"
  }
]
```

# Supported reply types

Please refer to the [HTTP API](/en/article/http-api-overview-1bpn7li/) to learn about supported reply types.

|| You can also use your own types if you have custom implementation of payload parsing using Android and iOS SDKs
