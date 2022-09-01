---
description: Let's help Agents improve
---

# Downvote Agent Responses

Machine learning is cool, but it certainly isn’t perfect. With this in mind, we’ve created a fast and easy way for you to downvote an agent’s response if it doesn’t quite make sense, or contains something offensive/inappropriate.

First, get the **‘tid’** from your agent’s /chat response. Got that? Great. Now all you need to do is ping our API endpoint with your ‘**tid’** and your **api key.**

Here’s a Python example:

```
import requests
r = requests.post('https://api.carterapi.com/v0/downvote', json={
   'api_key': 'YOURAPIKEY',
   'tid': "YOUR TID",
})
```

And here is a javascript example:

```
fetch(server + "/v0/downvote", {
               method: "POST",
               headers: {
                   Accept: "application/json",
                   "Content-Type": "application/json",
               },
               body: JSON.stringify({
                   api_key: ‘YOUR API KEY,
                   tid: ‘YOUR TID’,
               }),
           });

```

### **But wait! Why would I do this?**

Every month, we retrain your Carter agent to better understand what to say and what not to say using this feedback. This means our agents will get better and better overtime, and the more people that use the service, the faster this happens.



Got a question or something you want changed? Head over to [<mark style="color:purple;">Discord.</mark>](https://discord.com/invite/YqWwCVU8UH)<mark style="color:purple;"></mark>
