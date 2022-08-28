---
description: Sounds awesome....what is it?
---

# Custom Triggers

Custom Triggers allow you to clearly detect what the player/user is talking about by learning from a few example phrases. With this you can steer the conversation a certain way and even make something happen within your game or application.

{% embed url="https://www.youtube.com/embed/G_PP9kDwIRg" %}
A video walkthrough.
{% endembed %}

To get started, simply go to the 'Custom Triggers' tab on your agent's page and select the '+ New Trigger' button. You will be presented with a popup asking for three main pieces of information.&#x20;

* **Name** - This is how your trigger will be labelled and potentially how your project will identify what has been triggered. With that in mind, we recommend keeping them self-explanatory and easy to work with. _'get-weather', 'next-village'_ etc.
* **Examples** - We recommend a minimum of 5 example phrases for your agent to learn from. These should represent different ways to say the phrase, for example: _"what is the weather?", "can you tell me the weather?", "I'd like to know the weather."_
* **Responses** - If you leave this blank, your agent will reply with whatever it thinks is best, however if you wish to have your agent say something specific, you can add a few custom responses to steer the conversation a certain way or simply keep the conversation in-keeping with your game/application.

Once you've created your custom trigger, you will be able to edit it by selecting the 'down arrow' from the custom triggers table. Here you will see all of the above as well as two new items.

* **Threshold** - This represents, as a percentage, how confident you want your agent to be before activating the custom trigger. For example, 99% would almost never be triggered unless someone says a phrase that exactly matches one of your example phrases. A threshold of 0% would lead the agent to activate the custom trigger in most cases, leading to a bad user experience. We recommend starting at 50% and slightly moving either up or down to get the best performance.
* **Metadata** - A new addition to the Carter service. Metadata allows you to return custom data in the JSON format. This could be a script your project needs to run, how many coins to deduct from a player if they say a certain thing, or anything your application needs!
