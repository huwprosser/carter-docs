# Overview

Plugins allow you to extend the functionality of an agent. They can be used to make the agent more useful, more interesting to talk to, or better suited to helping you with a specific task.

{% hint style="info" %}
Plugins are a successor to [webhooks-deprecated.md](../integrations/webhooks-deprecated.md "mention"). Webhooks allow you to detect when a forced behaviour is triggered.
{% endhint %}

## Why Use Plugins?

There are a few reasons why you might want to use plugins:

* to enable access to a live data source such as the weather or a news feed
* to enable an agent to perform actions on your behalf, such as sending messages or setting a reminder
* to create a forced response to a trigger in a conversation

## Discover Plugins

To discover new plugins created by the community, visit #plugins on the Carter Discord server.

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
