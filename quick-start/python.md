---
description: Get started adding Carter to your Python project!
---

# Python

1. Create your character in the Controller at [https://controller.carterlabs.ai](https://controller.carterlabs.ai/).
2. Install the requests library for Python. You can install it using pip by running `pip install requests`.
3. Use the following code to send a message to your character:

```python
import requests
import json

response = requests.post("https://api.carterlabs.ai/api/chat", headers={
    "Content-Type": "application/json"
}, data=json.dumps({
    "text": "MESSAGE YOU WANT TO SEND",
    "key": "YOUR API KEY",
    "user_id": "UNIQUE USER ID" # THIS CAN BE ANYTHING YOU WANT!
    "speak": True # DEFAULT FALSE | FOR VOICE OUTPUT
}))

print(response.json())

```

4. Replace "YOUR API KEY" with the API key you received when you created your character in the online studio. **Treat this as a password. Anyone can talk to your agent with this key!**
5. Replace "UNIQUE USER ID" with a unique ID for your user. This can be any string you want.
6. Replace "MESSAGE YOU WANT TO SEND" with the message you want to send to your character.
7. The response from your character will be returned as a JSON object. You can access the response message and any forced behaviours from the JSON object.

That's it! You're now ready to start building your own interactions with your Carter character in Python.

\`\`
