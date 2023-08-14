---
description: This feature is currently experimental.
---

# /personalise

{% hint style="warning" %}
**Sunset Notice** — **API**

We are sunsetting our public API on 01 September 2023. All characters are alive and waiting in [Carter Chat](https://carter.chat).

Read the full notice: [sunset-notice.md](sunset-notice.md "mention")
{% endhint %}

Transform any piece of text into something your Character would say. For example, imagine we want our London taxi driver character to say "Hello", our personalise endpoint will return:\
\
"Alright mate!"

{% swagger src="https://api.carterlabs.ai/openapi.json" path="/personalise" method="post" %}
[https://api.carterlabs.ai/openapi.json](https://api.carterlabs.ai/openapi.json)
{% endswagger %}

```python
import requests
import json

reqUrl = "https://api.carterlabs.ai/personalise"

headersList = {
 "Accept": "*/*",
 "Content-Type": "application/json" 
}

payload = json.dumps({
  "key": "API KEY",
  "text": "Hello",
  "user_id": "UNIQUE USER ID",
  "speak": False
})

response = requests.request("POST", reqUrl, data=payload,  headers=headersList)

print(response.content)
```

{% hint style="warning" %}
**Important**: See [user-id-best-practices.md](../concepts/user/user-id-best-practices.md "mention") to learn how to choose a good `user_id` value.
{% endhint %}
