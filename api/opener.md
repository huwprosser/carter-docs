---
description: This feature is currently experimental.
---

# /opener

Generate a conversation opener tailored to your [Player](../concepts/user/) by simply providing your API key and the Player ID.

```python
import requests
import json

reqUrl = "https://api.carterlabs.ai/opener"

headersList = {
 "Accept": "*/*",
 "Content-Type": "application/json" 
}

payload = json.dumps({
  "key":"YOUR API KEY",
  "user_id": "USER ID",
  "personal": True || False # use to use character memory to enhance the opener. Default = True
})

response = requests.request("POST", reqUrl, data=payload,  headers=headersList)

print(response.text)
```
