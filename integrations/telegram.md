---
description: Talk to your character on Telegram!
---

# Telegram

If you've built a [character](../concepts/characters/) with Carter and want to carry on the conversation you can, via our easy to use Telegram integration.\


### Step 1 - Create a Telegram Bot

<div align="left">

<figure><img src="../.gitbook/assets/fdcc7b6d5fb3354adf.jpg" alt=""><figcaption></figcaption></figure>

</div>

Open up Telegram and search for "BotFather", this is an assistant built into Telegram that lets you create bots on their service. To get started type "/start", The BotFather will then walk you through the process.\
\
Once you've completed the conversation you will be given a Telegram access token.&#x20;

**Keep this safe.**&#x20;

### Step 2 - Connect your bot to Carter

We're working on a better integration of this feature in the [controller](https://controller.carterlabs.ai), but for now the following code will allow you to do this. \
\
<mark style="color:blue;">**You only need to run this once.**</mark>

```python
import requests
import json

reqUrl = "https://api.carterlabs.ai/connect-telegram"

payload = json.dumps({
  "key": "YOUR API KEY",
  "telegram_key": "YOUR TELEGRAM ACCESS TOKEN"
})

response = requests.request("POST", reqUrl, data=payload,  headers={
   "Content-Type": "application/json" 
})

print(response.text)
```

### Step 3 - Start talking & sharing!

If all is well, you should now be able to search for your Telegram Bot and start talking to your Carter Character through it! What's more, if you want to reconnect your telegram bot to another character you can simply run the above code again.\
\
Your Carter Character is now available to the public. Share what you create easily with anyone on Telegram!

### Disconnecting from Telegram

To disconnect simply run the code above with "-" as the API key.
