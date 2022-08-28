---
description: Get talking to your agent ASAP.
---

# 🚀 Quick Start Guide

Let's just dive right in. To get started with Carter in your project you need&#x20;

### **Step 1**

Sign up to Carter and create a new agent. You can learn more about this in the [Dashboard Docs](dashboard/).

### **Step 2**

Now you want to chat with your agent right? This is pretty simple as Carter agents live behind a standard REST API endpoint.&#x20;

<details>

<summary>cURL</summary>

You could send a simple cURL request like this:

```
curl --location --request POST 'https://api.carterapi.com/v0/chat' \
--header 'Content-Type: application/json' \
--data-raw '{
    "api_key": "MY API KEY",
    "query": "MY MESSAGE TO CARTER",
    "uuid": "A UNIQUE USER ID"
}'
```



</details>

<details>

<summary>Python Example</summary>

```python
import requests
import json

url = "https://api.carterapi.com/v0/chat"

payload = json.dumps({
  "api_key": "MY API KEY",
  "query": "MY MESSAGE TO CARTER",
  "uuid": "A UNIQUE USER ID"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```



</details>

### **Step 3**

You probably want to get your head around the JSON response right? See[ here](carter-api/api-response.md) for a full breakdown or skip to:

* [Downvoting agent responses (help improve Carter)](carter-api/downvote-agent-responses.md)
* [Using you Carter Agent's Voice](carter-api/voice-api.md)
* [Get started with these example projects! (Unity, Python and more!)](examples/)

\
Show us what you're building via our community on Discord!
