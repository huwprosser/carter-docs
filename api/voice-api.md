---
description: Quick guide on using the Voice API
---

# Voice API

Text chats are cool but they’re not quite the experience we’re looking for, that’s why we’re working on as many audio tools as possible.

Voice Recognition is coming soon. But for now let’s focus on Text-to-speech (making your agent speak).

In your agent response you will find **output.audio** - a URL that will stream back an mp3 of your agent saying anything you want.

### Unity&#x20;

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

### **JavaScript**

In Javascript you can use this really easily with the Audio Object. Like this:

```
//assuming you have your agent’s response
var myAudio = new Audio(agent_response.output.audio);
myAudio.play()
```

### **Python**

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



Got a question or something you want changed? Head over to [<mark style="color:purple;">Discord.</mark>](https://discord.com/invite/YqWwCVU8UH)<mark style="color:purple;"></mark>
