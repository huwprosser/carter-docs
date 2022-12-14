---
description: Let's take a look at the API response
---

# Chat

### Diving into your agent’s responses

Every time you send a message to your agent, you get a reply. This contains a large range of useful tools that can be used to build powerful experiences, much more powerful than just a simple chatbot. Let’s have a look at a typical API response:

```
r = {
    'input': 'Hello Carter agent!',
    'triggers': [
        {
            'type': 'greeting', 
            'score': 0.94, 
            
            // OPTIONAL - Activate entity recognition to extract names, dates etc.
            'entities': [
                {
                    label:"location",
                    word:"london",
                    confidence: 0.9
                }
            ],
            
            // OPTIONAL - return custom data with each custom trigger
            'meta': {
                "foo":"bar"
            },
            
            // OPTIONAL - data requested from the user in triiger requirements
            'data' : {
                "foo":"bar"
            }
        }
    ],
    'question': False,
    'output': {
        'text': "Hey human player!",
        'supplier': 'tr-pc',
        'voice': 'https://api.carterapi.com/v0/speak/GZAnnd57N5GZNouS9hKEp7dSBu/Hey Human Player!'
    },
    'sentiment': {
        'input': { 
            'label': 'POS',
            'confidence': 0.9
        },
        'output': { 
            'label': 'NEG',
            'confidence': 0.8
        },
        'conversation': { 
            'label': 'NEU',
            'confidence': 0.6
        },
    },
    'time_taken': 2.023,
    'credits_used': 3,
    'tid': '165874259062c56d9d85f9033thya555c84',
    
    // OPTIONAL - returned when agent is gathering information for a custom trigger's requirements.
    'information_request': true
    
}
```

so what does this mean? Let's break it down:

**input:** The text given to the agent from the user.&#x20;

****[**triggers**](../agents/custom-triggers/)**:** A list of custom triggers that have been activated by the user. These can be used to give canned responses, get information from the user, trigger in-game actions and detect names, places etc.

**question:** If the user asked a question or not. Useful if you’re trying to do any post processing or want to log it as metadata in your own database!&#x20;

**output:** Contains any “human-understandable” response from your agent, both audio and text.&#x20;

**output.text:** The text generated by the Carter agent, this could be a canned response from a custom trigger, or it could be AI generated.&#x20;

**output.supplier:** A simple string to track the type of response and to help us diagnose issues internally. output.audio: A web url of the text output as speech in your agent’s voice. This can be played, for example, using a JavaScript Audio Object.&#x20;

**sentiment:** Allows you to measure the sentiment of the conversation.&#x20;

**sentiment.input:** Shows whether the user’s input is positive or negative (sentiment.input.label) as well as a confidence score (sentiment.input.score)&#x20;

**sentiment.output (Coming Soon):** Shows whether the agent’s output is positive or negative (sentiment.output.label) as well as a confidence score (sentiment.output.score)&#x20;

**sentiment.conversation (Coming Soon):** Shows whether the entire conversation is positive or negative (sentiment.conversation.label) as well as a confidence score (sentiment.conversation.score).&#x20;

**time\_taken:** The amount of time it took to process your request, over time, this metric will hopefully go down as the service gets more efficient!&#x20;

**credits\_used:** How many tokens your request used. Useful for usage and cost analysis tracking.&#x20;

**tid:** A unique identifier for this turn (the request you sent to the API). This can be used to get support on an exact agent response or to use with our new Downvote feature!

**information\_request:** Only returned if the user has activated a custom trigger that requires follow-up questions to be asked. Useful if needing to disabled wake-word detection temporarily etc.



Got a question or something you want changed? Head over to [<mark style="color:purple;">Discord.</mark>](https://discord.com/invite/YqWwCVU8UH)<mark style="color:purple;"></mark>
