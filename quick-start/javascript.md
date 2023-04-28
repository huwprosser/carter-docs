---
description: Get started adding Carter to your JavaScript project!
---

# JavaScript

1. Create your character in the Controller at [https://controller.carterlabs.ai](https://controller.carterlabs.ai/).
2. Use the following code to send a message to your character:

```javascript
const data = {
  text: 'MESSAGE YOU WANT TO SEND',
  key: 'YOUR API KEY',
  playerId: 'UNIQUE USER ID (THIS CAN BE ANYTHING YOU WANT!)',
  speak: true // DEFAULT FALSE | FOR VOICE OUTPUT
};

fetch('https://api.carterlabs.ai/chat', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(data),
})
  .then(response => response.json())
  .then(data => {
    console.log('Input:', data.input);
    console.log('Output Text:', data.output.text);

    data.forced_behaviours.forEach(fb => {
      console.log('Forced Behaviour:', fb.name);
    });
  })
  .catch(error => {
    console.error(error);
  });

```

4. Replace "YOUR API KEY" with the API key you received when you created your character in the online studio. **Treat this as a password. Anyone can talk to your agent with this key!**
5. Replace "UNIQUE USER ID" with a unique ID for your player. This can be any string you want.
6. Replace "MESSAGE YOU WANT TO SEND" with the message you want to send to your character.
7. The response from your character will be returned as a JSON object. You can access the response message and any forced behaviours from the JSON object.

That's it! You're now ready to start building your own interactions with your Carter character in JavaScript.

\
**😎 Our community builds neat stuff. Including CarterJS.**

{% embed url="https://github.com/LazyLyrics/carter-js" %}
