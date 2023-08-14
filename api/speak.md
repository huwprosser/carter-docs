---
description: Text-to-speech when you need it. (Beta)
---

# /speak

{% hint style="warning" %}
**Sunset Notice** — **API**

We are sunsetting our public API on 01 September 2023. All characters are alive and waiting in [Carter Chat](https://carter.chat).

Read the full notice: [sunset-notice.md](sunset-notice.md "mention")
{% endhint %}

Our[ /chat](chat.md) endpoint already supports text-to-speech out of the box by simply providing `speak: true` in your request. This however impacts latency. That's why we're now supporting stand-alone speech requests that will use your character's same voice.

{% swagger src="https://api.carterlabs.ai/openapi.json" path="/speak" method="post" %}
[https://api.carterlabs.ai/openapi.json](https://api.carterlabs.ai/openapi.json)
{% endswagger %}

<details>

<summary>Python Example</summary>

```python
import requests

def speak(toSay):
    url = "https://api.carterlabs.ai/speak"
    headers = {"Content-Type": "application/json"}
    data = {
        "text": "HELLO CARTER",
        "key": "YOUR API KEY"
    }
    
    try:
        response = requests.post(url, headers=headers, json=data)
        response.raise_for_status()
        data = response.json()
        print(data["file_url"])  # Print the file URL
        
        # Play audio from URL (you will need to implement this part)
        # You can use libraries like pydub or playsound to play the audio
        
    except requests.exceptions.RequestException as e:
        print("Error:", e)

```

</details>

<details>

<summary>JavaScript (Browser)</summary>

```javascript
fetch("https://api.carterlabs.ai/speak", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
        text: "HELLO CARTER",
        key: "YOUR API KEY"
    }),
})
.then((response) => response.json())
.then((data) => {
    console.log(data.file_url);

    // play audio from url
    const audio = new Audio(data.file_url);
    audio.play();
})
```

</details>
