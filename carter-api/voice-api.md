---
description: Quick guide on using the Voice API
---

# Voice

Text chats are cool but they’re not quite the experience we’re looking for, that’s why we’re working on as many audio tools as possible.

### The Basics

You can use your agent's voice to say anything using the following URL:

```
https://api.carterapi.com/v0/speak/YOURAPIKEY/TEXT-TO-SPEAK
```

This service is still in early beta and may change regularly.&#x20;

### Integration

We pre-fill the above API endpoint for you in each API response from your agent. You will find **output.audio** - a pre-filled URL that, when played, will stream back an mp3 of your agent saying it's response **output.text** response. In the following examples we use this URL with the assumption that you're using the [Chat API ](api-response.md)end point, this is not a requirement.

<details>

<summary>Unity (C#)</summary>

Pass your agent’s response **output.audio** to this method.

```
IEnumerator PlayAudio(string url)
    {
        using (UnityWebRequest www = UnityWebRequestMultimedia.GetAudioClip(url, AudioType.MPEG))
        {
            yield return www.SendWebRequest();

            if (www.result == UnityWebRequest.Result.ConnectionError)
            {
                Debug.Log(www.error);
            }
            else
            {
                AudioClip myClip = DownloadHandlerAudioClip.GetContent(www);
                AudioSource audioSource;
                audioSource.clip = myClip;
                audioSource.Play();
            }
        }
    }
```



</details>

<details>

<summary>JavaScript</summary>

In Javascript you can use this really easily with the Audio Object. Like this:

```
//assuming you have your agent’s response
var myAudio = new Audio(agent_response.output.audio);
myAudio.play()
```



</details>

<details>

<summary>Python</summary>

We’re working on creating an easier way to do this, but for now:

```
pip install playsound

r = requests.get(agent_response.output.audio, stream=True)
with open('temp.mp3', 'wb') as f:
for chunk in r.iter_content(chunk_size=1024):
     		if chunk:
          		f.write(chunk)
                    
playsound('temp.mp3')           
# remove temp file
os.remove('temp.mp3')
```



</details>



Got a question or something you want changed? Head over to [<mark style="color:purple;">Discord.</mark>](https://discord.com/invite/YqWwCVU8UH)<mark style="color:purple;"></mark>
