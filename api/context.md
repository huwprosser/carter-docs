---
description: Keep your agent up-to-date with the world around it.
---

# /context

{% hint style="warning" %}
**Sunset Notice** — **API**

We are sunsetting our public API on 01 September 2023. All characters are alive and waiting in [Carter Chat](https://carter.chat).

Read the full notice: [sunset-notice.md](sunset-notice.md "mention")
{% endhint %}

The Context API lets programmers provide their agents with separate _context prompts_, helping it understand what's going on in the conversation and the world around it.&#x20;

**What Are Context Prompts?**

Context prompts are short pieces of information that set the scene or provide relevant facts for your conversation. Here are some examples:

* **Scene Setting**: Tell the agent where your chat is happening.
  * Example: "The chat is happening in front of the castle"
* **What the Agent Sees**: Mention something the agent can 'see' in the chat.
  * Example: "{agent\_name} can see a dog"
* **Character Action**: Share an action or event that happened during the chat.
  * Example: "Tony just received a text message"
* **Where You're Chatting**: Mention how you're communicating with the agent.
  * Example: "{agent\_name} and Huw are chatting on Discord"

**Rules for Using Context Prompts**

To use the Context API effectively, please follow these rules:

* Context prompts should be no more than 128 characters long.
* You can't send more than three context messages consecutively.
* For more accurate context, use the "context" parameter when sending a message via the [/chat](chat.md) endpoint. This helps you insert context exactly where you need it.

**Integration Tips**

* For context info that isn't related to time, use this dedicated /context endpoint. This ensures your context prompts integrate seamlessly and keeps the chat flow going.
* You can use the {agent\_name} placeholder in context prompts. The system will automatically replace it with the agent's name.



{% swagger src="https://api.carterlabs.ai/openapi.json" path="/context" method="post" %}
[https://api.carterlabs.ai/openapi.json](https://api.carterlabs.ai/openapi.json)
{% endswagger %}
