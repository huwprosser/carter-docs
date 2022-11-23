---
description: Ask follow-up questions before activating your triggers.
---

# Requirements

Conversational steering with Carter's custom triggers is awesome, but sometimes you need to ask follow up questions before making something happen in your application such as "Which colour sword would you like?" or "Which lights would you like me to turn off?". Custom Trigger requirements allow you to add follow-up questions to collect this data and then return it to your application along with the activated custom trigger. \
\
Your agent will block all other conversation until the trigger's requirements are answered by the user.

<figure><img src="../../.gitbook/assets/screely-1669163095892.png" alt=""><figcaption></figcaption></figure>

You can add as many requirements as you want to your custom triggers. Simply edit your custom trigger and navigate to the "Requirements" tab. Here you can add a requirement:\
\
\- Name (The name of the requirement, used as the JSON key in the API response)\
\- Request Phrase (How your agent will ask the human for the information)\
\- Type (The type of data, currently we only allow the collection of the raw human response)\
\
Click "confirm" and save your custom trigger's changes. Once your agent is finished re-training, it will begin collecting the trigger's requirements before activating the custom trigger. Pretty neat. \
\
Stuck? Reach out to us on the Discord server!
