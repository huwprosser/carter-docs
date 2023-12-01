# Developer Commands

All Carter agents provide slash commands that can be used to interact with the Plugins system. To use developer commands, you must first become a developer with `/plugin dev start`. You can view a list of all available commands by typing `/help`.

{% hint style="info" %}
For a list of commands for plugin consumers, see [commands.md](../commands.md "mention").
{% endhint %}

*   `/plugin dev start`

    Become a plugin developer and view your developer ID.
*   `/plugin dev submit <URL>`

    Submit a new or updated plugin. `URL`: The URL of the plugin manifest file, e.g. `https://example.com/carterplugin.json`.
*   `/plugin dev publish <code>`

    Make the specified plugin public. `code`: The plugin code, e.g. `0001`.
*   `/plugin dev list`

    Display a list of the plugins that you have submitted.
*   `/plugin dev destroy <code>`

    Destroy a plugin that you have submitted, this will uninstall it from all relationships and release the plugin name to be used again. `code`: The plugin code, e.g. `0001`.
*   `/plugin dev token <code>`

    Display the secret token for the specified plugin.
*   `/plugin dev token reset <code>`

    Reset the secret token for the specified plugin.

{% hint style="warning" %}
At the current time, becoming a developer and submitting plugins is tied to your user (unique to each DM with our Discord bots, and unique to each combination of API Key and user ID). For this reason, **we strongly recommend you use a DM with a single Carter Discord bot for all developer operations**. We will soon provide a way to link existing users together to persist your developer information across platforms.
{% endhint %}
