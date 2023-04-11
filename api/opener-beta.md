---
description: This feature is currently experimental.
---

# /opener (beta)

Generate a conversation opener tailored to your [Player](../concepts/players.md) by simply providing your API key and the Player ID.

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
  "playerId": "PLAYER ID"
})

response = requests.request("POST", reqUrl, data=payload,  headers=headersList)

print(response.text)
```
