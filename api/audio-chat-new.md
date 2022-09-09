---
description: EARLY BETA
---

# Audio Chat (NEW!)

```
https://api.carterapi.com/v0/audio-chat
```

The Audio Chat API allows you to send audio files to your [Carter agent](../dashboard/agents/) and get insights as well as a conversational response back.&#x20;

<figure><img src="../.gitbook/assets/Audio Chat.png" alt=""><figcaption><p>Audio Chat API</p></figcaption></figure>

Our audio endpoint first converts human speech into text and passes it to the [Carter agent](../dashboard/agents/), resulting in the same response as our[ Chat endpoint](../carter-api/api-response.md).

To start using the audio endpoint you need to upload audio as a file to our POST end point.&#x20;

**A few things to consider:**

* We currently accept 16000Hz files in WAV format.
* We highly recommend sending short, sentence long, audio files for acceptable response times.

Implementing the collection of audio is completely up to the developer and the experience they're building. We recommend a "push-to-talk" experience as a good starting place or even the use of voice activity detection to isolate when someone is talking and package it up for consumption via our API. You can find our example Unity project [here](https://github.com/huwprosser/carter-unity-voice-demo).&#x20;

<details>

<summary>C#</summary>

```csharp
        WWWForm form = new WWWForm();
        form.AddBinaryData("file", data, "aud.wav");
        form.AddField("api_key", apiKey);
        form.AddField("uuid", uuid);

        UnityWebRequest www = UnityWebRequest.Post("https://api.carterapi.com/v0/audio-chat", form);
        yield return www.SendWebRequest();

        if (www.result != UnityWebRequest.Result.Success) {
            Debug.Log(www.error);
        }
        else {
            var response = www.downloadHandler.text;            
            Debug.Log(response);
        }

        www.Dispose();
```

</details>

We are actively looking for more community projects using this endpoint! Let us know via **huw@carterapi.com**
