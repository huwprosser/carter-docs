---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Overview

We spawned in the depths of the developer community. After a solid amount of time serving an API it became clear that developers on Carter were building some amazing characters, loving talking to them, but had no way to share them.&#x20;



We launched [carter.chat](https://carter.chat) to let anyone meet, create and spend time with characters. Our recent advances in memory, dialogue and emotional intelligence now allow for more meaningful, long-term relationships with them.&#x20;



### Are developers out?

Absolutely not. You can still extend the capabilities of your characters by building plugins. Plugins give your characters special abilities. They can be used to make the character more useful, more interesting to talk to, or better suited to helping you with a specific task.



### Why Use Plugins?

There are a few reasons why you might want to use plugins:

* Enable access to a live data source such as the weather or a news feed
* Allow a character to perform actions on your behalf, such as sending messages or setting a reminder
* Create custom responses to certain topics.

## Install and Use Plugins

Plugins can be managed on a per-relationship basis. A relationship is between a person and an agent. This means that a plugin added to one relationship will not be available when you talk to a different agent, nor for anyone else that interacts with the same agent.

To use a plugin, you must first add it to your relationship. You can do this using [commands.md](commands.md "mention") in a chat with the agent.

Example of installing a new plugin:

> **/plugin install 0001**
>
> _Are you sure you want to install "Awesome ToDo" by "John Doe"? (yes/no)_
>
> **yes**
>
> Plugin installed.

Once a plugin is installed, it will be used automatically when the agent decides it is appropriate to do so. For example, if you have a weather plugin installed, the agent may use it to respond to a question about the weather. See the plugin developer's documentation for the plugin to find out what it can do.
