---
description: Full walkthrough from Sign Up to having a trained and deployed Carter Agent.
---

# Quick Start Guide

Let's just dive right in. To get started with Carter in your project you need&#x20;

**Step 1**

Sign up to Carter and create a new agent. You can learn more about this in the [Dashboard Docs](dashboard/).



**Step 2**

Now you want to chat with your agent right? This is pretty simple as Carter agents live behind a standard REST API endpoint. \
\
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

Or if cURL isn't your thing how about Python?

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

