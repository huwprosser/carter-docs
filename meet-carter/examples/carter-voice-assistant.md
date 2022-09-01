---
description: Talk to your Carter agent with voice input and output
---

# Carter Voice Assistant

An example project showing how to use [www.carterapi.com](http://www.carterapi.com/) as a voice assistant. It uses LOCAL speech recognition to get the user's voice input, and then uses the Carter API to get the response. It also uses the Carter API to get the agent's voice output.

### A note on speech recognition:

This demo used the out-of-the-box wave2vec2 without a n-gram model. This is a very simple model, and it is not recommended for use in production due to its accuracy limitations. Carter API will soon provide a, more accurate, cloud-based speech recognition model.

### Get Started:

To get started, go to [<mark style="color:purple;">https://github.com/huwprosser/carter-voice-assistant</mark>](https://github.com/huwprosser/carter-voice-assistant)<mark style="color:purple;"></mark>

install the requirements listed in the \`requirements.txt\` file by running:

`pip install -r requirements.txt`

Then, run the following command to start the server:

`python app.py --key your-api-key --voice True`

To find out more about the API key and configure your agent, visit the <mark style="color:purple;"></mark> [<mark style="color:purple;">Carter API</mark>](https://www.carterapi.com/).

### Known Issues:

\- M1 Mac doesn't seem to support PyAudio.

* Speech-to-text Performance is not optimized and could be optimized in conjunction with n-grams.
* Speed could be improved.
