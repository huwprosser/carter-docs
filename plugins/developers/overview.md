# Developer Overview

Plugins allow you to extend the functionality of an agent. They can be used to make the agent more useful, more interesting to talk to, or better suited to helping you with a specific task.

## Why Use Plugins?

There are a few reasons why you might want to use plugins:

* to enable access to a live data source such as the weather or a news feed
* to enable an agent to perform actions on your behalf, such as sending messages or setting a reminder
* to create a forced response to a trigger in a conversation

## How Do They Work?

When in conversation, the agent will be continually checking if any of its Plugins are suitable for the current situation. If at any point it decides that a plugin is required, it will call one of its API endpoints to get a response. The agent will then use the data or the forced response to respond to the user.

If the agent wants to use an API but does not have all the required information to populate the API inputs, it will ask the user for the information it needs.

## Examples

In the following examples, we'll use a pirate-themed agent with a weather plugin enabled to demonstrate the way Plugins can be used to augment the conversation.

<details>

<summary>Weather Plugin manifest file</summary>

Some fields are omitted for brevity.

```json
{
  "name_for_human": "Weather",
  "description_for_human": "A plugin for getting weather information.",
  "api": {
    "base_url": "https://weather.example.com",
    "endpoints": [
      {
        "name": "get_current",
        "description": "Get the current weather for a location.",
        "path": "/current",
        "method": "POST",
        "input": [
          {
            "name": "location",
            "description": "The general location on Earth to get the weather for. Can be a country, city, town, or other location identifier."
          }
        ],
        "output": [
          {
            "name": "temperature_deg_c",
            "description": "The temperature of the location in degrees celcius."
          },
          {
            "name": "precipitation",
            "description": "A description of the precipitation condition."
          }
        ]
      },
      {
        "name": "weather_warnings",
        "description": "Get weather warnings for a location.",
        "path": "/warnings",
        "method": "POST",
        "input": [
          {
            "name": "location",
            "description": "The general location on Earth to get weather warnings for. Can be a country, city, town, or other location identifier."
          }
        ],
        "output": [
          {
            "name": "weather_warnings",
            "description": "A description of the weather warnings for the location."
          }
        ]
      }
    ]
  }
}
```

</details>

### Example 1: No plugin suitable

1.  The user asks a question that does not require a plugin.

    > _User:_ How are you?
2.  The agent does not have a plugin for this task, and so will respond as usual.

    > _Agent:_ Ahoy, matey! Me be feelin' as fine as a ship in fair winds! And how be ye, ye scurvy dog?

### Example 2: Weather plugin suitable

1.  The user asks for the weather.

    > _User:_ What's the weather like today in London?
2. The agent will check its plugins, and find that the weather plugin is suitable for this request.
3.  The agent calls the Weather Plugin's `get_current` API endpoint with the location set to "London", which returns the current weather.

    ```json
    {
      "success": true,
      "data": {
        "temperature_deg_c": 5,
        "precipitation": "heavy rain"
      }
    },
    ```
4.  The agent will then respond to the user, using the current weather to inform its response.

    > _Agent:_ Arr matey, the weather in London be a chilly 5 degrees Celsius, with a heavy rain pourin' down from the skies. Best be bringin' yer raincoat and galoshes if ye be venturin' out today, arrr!

### Example 3: Weather plugin with more information required from the user

1.  The user asks for the weather.

    > _User:_ What's the weather like today?
2. The agent will check its plugins, and find that the weather plugin is suitable for this request.
3.  The agent can see that the user has not specified a location (which is required by the Plugin), and so will ask the user for a location.

    > _Agent:_ Ahoy matey! Which port o' call be ye seekin' the weather fer? Let me know the location, and I'll fetch ye the forecast, arr!
4.  The user specifies a location

    > _User:_ Dublin
5.  The agent calls the Weather Plugin's current weather API endpoint which returns the weather for today.

    ```json
    {
      "success": true,
      "data": {
        "temperature_deg_c": 10,
        "precipitation": "none"
      }
    },
    ```
6.  The agent will then respond to the user, using the current weather to inform its response.

    > _Agent:_ Arr matey, the weather in Dublin be a fine 12 degrees Celsius, and nay a drop of precipitation in sight! Ye'll be enjoyin' a fair day on the high seas, or in this case, the streets of Dublin! Har har har!

### Example 4: Weather plugin with forced response

The weather Plugin also has a weather warnings API endpoint which uses a forced response to ensure that the agent responds verbatim, without personalisation.

1.  The user asks for the weather.

    > Are there any weather warnings today in London?
2. The agent will check its plugins, and find that the weather warnings API endpoint in the weather plugin is suitable for this request.
3.  The agent makes a request to the weather warnings endpoint which includes a forced response in its response data.

    ```json
    {
      "success": true,
      "data": {
        "weather_warnings": [
          {
            "type": "thunderstorm",
            "severity": "yellow",
            "description": "Heavy showers and thunderstorms will develop..."
          }
        ]
      },
      "forced_response": "Heavy showers and thunderstorms will develop..."
    },
    ```
4.  The agent will then respond to the user with the forced response only.

    > _Agent:_ Heavy showers and thunderstorms will develop...
5.  The user asks for more information.

    > _User:_ What severity is that warning?
6.  The agent can still see the data that was returned from the weather API, and so can respond with the severity.

    > _Agent:_ Arr, matey! That be a yellow severity warnin' for ye! Beware the heavy showers and thunderstorms, for they be mighty fierce!

***
