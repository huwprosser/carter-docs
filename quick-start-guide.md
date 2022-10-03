---
description: Get talking to your agent ASAP.
---

# Quick Start

Let's just dive right in. To get started with Carter in your project you need

### **Step 1**

Sign up to Carter and create a new agent. You can learn more about this in the [Dashboard Docs](dashboard/agents/).

### **Step 2**

Now you want to chat with your agent right? This is pretty simple as Carter agents live behind a standard REST API endpoint.

<details>

<summary>Unity (C#)</summary>

{% code lineNumbers="true" %}
```csharp
using UnityEngine.Networking;

...

WWWForm form = new WWWForm();
form.AddField("aquery", "YOUR MESSAGE TO CARTER!);
form.AddField("api_key", "YOUR-API-KEY);
form.AddField("uuid", "USER-ID");

UnityWebRequest www = UnityWebRequest.Post("https://api.carterapi.com/v0/chat", form);
yield return www.SendWebRequest();

if (www.result != UnityWebRequest.Result.Success) {
    Debug.Log(www.error);
}
else {
    var response = www.downloadHandler.text;          
    Debug.Log(response);
}

```
{% endcode %}

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

### **Step 3**

You probably want to get your head around the JSON response right? See[ here](carter-api/api-response.md) for a full breakdown or skip to:

* [Downvoting agent responses (help improve Carter)](carter-api/downvote-agent-responses.md)
* [Using you Carter Agent's Voice](carter-api/voice-api.md)
* [Get started with these example projects! (Unity, Python and more!)](examples/)

\
Show us what you're building via our community on Discord!
