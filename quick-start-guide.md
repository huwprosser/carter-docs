---
description: Get talking to your agent ASAP.
---

# Unity

Let's just dive right in. To get started with Carter in your Unity project you need to follow these steps.

### **Step 1**

Create your character in the Controller at [https://controller.carterlabs.ai](https://controller.carterlabs.ai).

### **Step 2**

Install the Carter Unity API package in your Unity project. You can find it at [https://github.com/Carter-Labs-Ltd/carter-unity-api.git](https://github.com/Carter-Labs-Ltd/carter-unity-api.git).

### **Step 3**

Add Carter to your Unity project!

<pre class="language-csharp"><code class="lang-csharp"><strong>using Carter;
</strong>
<strong>//...
</strong>
<strong>void Start()
</strong>{
    myAgent = gameObject.AddComponent&#x3C;Agent>();
    myAgent.url = "https://api.carterlabs.ai/chat";
    myAgent.key = "YOUR API KEY";
    myAgent.playerId = "UNIQUE PLAYER ID (can be anything you want!)";
    
    //every time a message is sent through from your agent
    myAgent.onMessage += (ApiResponse response) => {
    
        //what the player said
        Debug.Log("Input: " + response.input);
        
        // what the character said in response
        Debug.Log("Output Text: " + response.output.text);

        // any forced behaviours detected
        foreach (ForcedBehaviour fb in response.forced_behaviours) {
            Debug.Log("Forced Behaviour: " + fb.name);
        }
        
    };
}

//...

// send a message to your character
myAgent.Interact("MESSAGE YOU WANT TO SEND");
</code></pre>

* Replace "YOUR API KEY" with the API key you received when you created your character in the online studio. **Treat this as a password. Anyone can talk to your agent with this key!**
* Replace "UNIQUE USER ID" with a unique ID for your player. This can be any string you want.
* Replace "MESSAGE YOU WANT TO SEND" with the message you want to send to your character.
* The response from your character will be returned as a JSON object. You can access the response message and any forced behaviours from the JSON object.
