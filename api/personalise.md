---
description: This feature is currently experimental.
---

# /personalise

Transform any piece of text into something your Character would say. For example, imagine we want our London taxi driver character to say "Hello", our personalise endpoint will return:\
\
"Alright mate!"\
\
Usage is easy. Simply provide your Character's API key and the text you want to personalise.

```python
import requests
import json

reqUrl = "https://api.carterlabs.ai/personalise"

headersList = {
 "Accept": "*/*",
 "Content-Type": "application/json" 
}

payload = json.dumps({
  "key":"API KEY",
  "text": "Hello"
})

response = requests.request("POST", reqUrl, data=payload,  headers=headersList)

print(response.content)
```
