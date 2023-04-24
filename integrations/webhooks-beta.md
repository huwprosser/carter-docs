---
description: Connect your Carter character to anything...yup.
---

# Webhooks (beta)

With Web-hooks your API, service, heck even robot can receive messages from Carter when someone triggers a forced behaviour and generate a custom response to return back.\
\
**Possible use cases include, but are in no way limited to:**\
\- Building more complex apps on top of Carter hosted with Flask, FastAPI etc.\
\- Controlling hardware such as Raspberry Pi on a network.\
\- Building next-level experiences for your Carter users! \
\
Right now, webhooks will only communicate with your API when someone activates a forced behaviour.

<figure><img src="../.gitbook/assets/USER TALKS ABOUT (2).png" alt=""><figcaption></figcaption></figure>

Carter can even send the same message to as many webhook endpoints you want, allowing you to host multiple services for different tasks, or perhaps a fleet of internet enabled robots. \


### Adding a Webhook

This is similar to the [Telegram integration](telegram.md). For now, you can simply call `/webhook/add` with your API key and the URL you want Carter to send the data to.\
\
<mark style="color:blue;">**You only need to run this once.**</mark>

```python
import requests
import json

reqUrl = "https://api.carterlabs.ai/webhook/add"

payload = json.dumps({
  "key": "YOUR API KEY",
  "url": "YOUR WEBHOOK URL"
})

response = requests.request("POST", reqUrl, data=payload,  headers={
   "Content-Type": "application/json" 
})

print(response.text)
```

### Response

The response from Carter to your webhook will look like:

```python
{
    "agent": str, # NAME OF CHARACTER
    "behaviour": {
        "name": str, # NAME OF BEHAVIOUR TRIGGERED
    },
    "data": object, # ADDITIONAL DATA || NULL
    "input": str #USER INPUT AS TEXT
}
```

### Removing a Webhook

Call `/webhook/remove` with your API key and the URL you want to remove \
\
<mark style="color:blue;">**You only need to run this once for each endpoint you want to remove.**</mark>

```python
import requests
import json

reqUrl = "https://api.carterlabs.ai/webhook/remove"

payload = json.dumps({
  "key": "YOUR API KEY",
  "url": "YOUR WEBHOOK URL"
})

response = requests.request("POST", reqUrl, data=payload,  headers={
   "Content-Type": "application/json" 
})

print(response.text)
```

<details>

<summary>Webhook API Example (Python)</summary>

Below is a simple Python web server that sends an output object back to Carter.

1. First, run `pip install fastapi uvicorn`

<!---->

2. Then save the below code as  `webhook_test.py`

<!---->

3. `python webhook_test.py`

```python
from fastapi import FastAPI, Request

app = FastAPI()

@app.post("/webhook")
async def webhook_handler(request: Request):
    data = await request.json()
    print("WEBHOOK RECEIVED", data)
    return {"output": "Webhook received!"}


if __name__ == "__main__":
    import uvicorn

    uvicorn.run(
        "webhook_test:app", host="0.0.0.0", port=5001, reload=True
    )
```

</details>
