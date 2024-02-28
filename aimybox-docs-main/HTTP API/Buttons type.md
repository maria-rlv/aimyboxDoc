Buttons reply contains a collection of buttons to render.
Each button can be a **simple button** or a **link** to external URL.

There is a format of this reply type

```
{
  "type": "buttons",
  "buttons": [
    {"text": "Cancel"},
    {"text": "Details", "url": "https://someurl.com"},
    {"text": "Restart game", "payload": "/start"}
  ]
}
```

### Simple button

The tap on simple button just sends a text of this button as a new user request. User can use these buttons instead of speaking of next command.

### Payload button

The tap on simple button with payload sends the payload field content instead of button's title text.

### Link button

Every link button contains _url_ field with direct URL to the external resource like a website. If user presses this button an assistant should open this URL in a web browser.

