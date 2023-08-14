---
description: This feature is currently experimental.
---

# /opener

{% hint style="warning" %}
**Sunset Notice** — **API**

We are sunsetting our public API on 01 September 2023. All characters are alive and waiting in [Carter Chat](https://carter.chat).

Read the full notice: [sunset-notice.md](sunset-notice.md "mention")
{% endhint %}

Generate a conversation opener tailored to your [Player](../concepts/user/) by simply providing your API key and the Player ID.

{% swagger src="https://api.carterlabs.ai/openapi.json" path="/opener" method="post" %}
[https://api.carterlabs.ai/openapi.json](https://api.carterlabs.ai/openapi.json)
{% endswagger %}

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

{% hint style="warning" %}
**Important**: See [user-id-best-practices.md](../concepts/user/user-id-best-practices.md "mention") to learn how to choose a good `user_id` value.
{% endhint %}
