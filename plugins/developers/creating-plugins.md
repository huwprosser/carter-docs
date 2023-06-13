# Creating Plugins

## Introduction

Every plugin is composed of two parts, an API and a manifest definition. The API can be hosted anywhere on the Internet, and the manifest file describes where to find it and what it can do.

## API Request Format

Carter will make requests to your plugin's API with plugin inputs encoded as JSON in the body.

<table data-full-width="true"><thead><tr><th width="189">Property</th><th width="91">Type</th><th width="95">Always</th><th>Description</th></tr></thead><tbody><tr><td>relationship_token</td><td>string</td><td>Yes</td><td>A token that is unique to the relationship on which the plugin is installed. The user can access their token using a slash command, and use it to configure your service through your own interface.</td></tr><tr><td>data</td><td>object</td><td>Yes</td><td>Guaranteed to provide all required inputs, but may not include any or all optional inputs.</td></tr></tbody></table>

The request object may include additional fields in the future.

### Secret Token

To verify that a request to your plugin's API has come from Carter, we will include a secret token in the `X-Carter-Plugin-Secret-Token` header. You can access this token with the `/plugin dev token <code>` command. The value of the secret token does not change when submitting a plugin update.

You should check that this header is present and matches the value we have given you with every request to your API.

{% hint style="warning" %}
We will **not** send a secret token header when requesting your manifest file. Please ensure that your manifest file can always be accessed.
{% endhint %}

{% hint style="danger" %}
You should keep this token a secret, otherwise anyone will be able to make requests to your API. An easy way to do this is to keep the value stored in an environment variable. Check the documentation for the hosting platform you are using for the best way to inject private environment variables.
{% endhint %}

If you accidentally reveal the token, you can reset it with the `/plugin dev token reset <code>` command. Don't forget to update the value in your project.

### Examples

Below is the data for a request to an endpoint with all required inputs. In this example a request is made to an endpoint with all required inputs. `data.location` matches the name of the input defined in `api.endpoints.input.name`.

```json
{
  "relationship_token": "e12e85d2...",
  "data": {
    "location": "London"
  }
}
```

If there are no required inputs, `data` will be an empty object.

```json
{
  "relationship_token": "e12e85d2...",
  "data": {}
}
```

## API Response Format

Carter expects your plugin to respond with a JSON object that includes a `success` property. All other properties are optional.

<table data-full-width="true"><thead><tr><th width="181">Property</th><th width="101">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>success</td><td>boolean</td><td>Yes</td><td>Whether the plugin operation was successful. For example, if a weather plugin failed to retrieve the weather information, this should be <code>false</code>.</td></tr><tr><td>data</td><td>object</td><td>No</td><td>The data to be used to create an agent's response. Will be provided to the agent if and only if <code>success</code> is <code>true</code>. The top level properties in this object must match the output as described in the manifest. Any sub-objects may be structured in any way, however it is important that the properties are descriptively named so that the agent can understand the data. For example instead of <code>{ "value": "10" }</code>, prefer <code>{ "unread_email_count": "10" }</code>.</td></tr><tr><td>error</td><td>string</td><td>No</td><td>An error message that describes the issue that occurred. Will be provided to the agent if and only if <code>success</code> is <code>false</code>.</td></tr><tr><td>forced_response</td><td>string</td><td>No</td><td>A forced response message. If present, the agent will respond with only this. Context (<code>data</code> or <code>error</code>) will be provided to the agent for future messages in the conversation.</td></tr></tbody></table>

### Limits

Responses that exceed any of these limits **will be rejected**. Please ensure that your responses are as concise as possible.

<table><thead><tr><th width="218">Property</th><th width="235">Limit</th></tr></thead><tbody><tr><td><code>data</code></td><td>500 characters (as JSON)</td></tr><tr><td><code>error</code></td><td>500 characters</td></tr><tr><td><code>forced_response</code></td><td>500 characters</td></tr></tbody></table>

### Examples

Successful plugin response with weather data:

```json
{
  "success": true,
  "data": {
    "temperature_deg_c": 5,
    "precipitation": "heavy rain"
  }
}
```

Successful plugin response with weather data and a forced response:

```json
{
  "success": true,
  "data": {
    "temperature_deg_c": 5,
    "precipitation": "heavy rain"
  },
  "forced_response": "It's raining heavily in London."
}
```

Unsuccessful plugin response with error message:

```json
{
  "success": false,
  "error": "Weather service is temporarily unavailable."
}
```

## Manifest Format

Every plugin is defined by a manifest file that describes where to find the plugin API and what its capabilities are. Validate your manifest file against the schema [here](https://www.jsonschemavalidator.net/s/bUzIujo4).

<table data-full-width="true"><thead><tr><th width="242">Property</th><th width="90.5">Type</th><th>Required</th><th width="293">Example</th><th width="365">Description</th></tr></thead><tbody><tr><td>manifest_version</td><td>string</td><td>Yes</td><td>"1"</td><td>Manifest file version (current: "1").</td></tr><tr><td>developer_id</td><td>string</td><td>Yes</td><td>"646cd283be483c45b56b3a8f"</td><td>The ID of the developer releasing the plugin (see <a data-mention href="become-a-developer.md">become-a-developer.md</a>).</td></tr><tr><td>version</td><td>string</td><td>Yes</td><td>"1.0.0"</td><td>The version of your Plugin (semantic versioning format). Must be incremented before submitting an update to an existing plugin.</td></tr><tr><td>name</td><td>string</td><td>Yes</td><td>"weather"</td><td>The name that unqiuely identifies your plugin (cannot be changed).</td></tr><tr><td>name_for_human</td><td>string</td><td>Yes</td><td>"Joe's Awesome Weather"</td><td>The display name for humans.</td></tr><tr><td>name_for_machine</td><td>string</td><td>Yes</td><td>"weather"</td><td>The name that the system will see (only lowercase letters and underscores).</td></tr><tr><td>description_for_human</td><td>string</td><td>Yes</td><td>"Get up-to-date weather information for any location."</td><td>A simple description of the plugin for humans.</td></tr><tr><td>desscription_for_machine</td><td>string</td><td>Yes</td><td>"Get up-to-date weather information for any location."</td><td>A description that the system will see. Can be used to provide additional context that may be relevant to our plugin detection system. We recommend keeping this the same as <code>description_for_human</code> in simple cases.</td></tr><tr><td>author_name</td><td>string</td><td>Yes</td><td>"Joe Bloggs" or "My Company Ltd"</td><td>The name of the Plugin author (individual or organisation).</td></tr><tr><td>contact_email</td><td>string</td><td>Yes</td><td>"joe@example.com"</td><td>The contact email for support and moderation.</td></tr><tr><td>api</td><td>object</td><td>Yes</td><td></td><td>The API Specfication (described below).</td></tr></tbody></table>

### API Specification

The `api` property in the manifest file describes the API that the agent will use to communicate with the Plugin.

<table data-full-width="true"><thead><tr><th width="128">Property</th><th width="92">Type</th><th width="108">Required</th><th width="270">Example</th><th>Description</th></tr></thead><tbody><tr><td>base_url</td><td>string</td><td>Yes</td><td>"https://weather.example.com"</td><td>The base URL for all API endpoints</td></tr><tr><td>endpoints</td><td>array</td><td>Yes</td><td></td><td>The API endpoints (described below)</td></tr></tbody></table>

### Endpoints

The `api.endpoints` property in the manifest file descibes the API endpoints that the agent will use to communicate with the Plugin. Each endpoint represents a single piece of functionality. At least one endpoint is required, and you can define up to 15. If the agent uses your plugin, only one endpoint will be used at a time.

<table data-full-width="true"><thead><tr><th width="138.5">Property</th><th width="89">Type</th><th width="106">Required</th><th width="210">Example</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>string</td><td>Yes</td><td>"get_current"</td><td>The name that uniquely identifies this endpoint.</td></tr><tr><td>description</td><td>string</td><td></td><td>"Get the current weather for a location."</td><td>A description of what this endpoint does.</td></tr><tr><td>path</td><td>string</td><td>Yes</td><td>"/current"</td><td>The path to the endpoint.</td></tr><tr><td>method</td><td>string</td><td>No</td><td>"POST"</td><td>The HTTP method that the API request will use. Can be "GET" or "POST" (default: "POST"). See why we recommend using POST below.</td></tr><tr><td>input</td><td>array</td><td>Yes</td><td></td><td>The inputs that this endpoint accepts. 0-3 inputs allowed.</td></tr><tr><td>output</td><td>array</td><td>Yes</td><td></td><td>The outputs that this endpoint provides. 0-10 outputs allowed.</td></tr></tbody></table>

#### Method

You can choose to allow either `GET` or `POST` requests for each API endpoint (`api.endpoints.method`). (Default: `POST`)

> Note: We recommend using `POST` for all endpoints. We only send input data in the body of the request, which some older web servers and proxies may drop on `GET` requests. Additionally, `GET` requests are more likely to be cached by proxies and web browsers, which could cause unexpected behaviour.
>
> If you decide to use `GET`, we suggest adding a `Cache-Control` header to prevent caching.
>
> ```
> Cache-Control: no-store, no-cache, must-revalidate, proxy-revalidate
> ```

### Inputs

The `api.endpoints.inputs` property in the manifest file describes the input values that the endpoint accepts. You can have up to three inputs per endpoint, each optionally required. We guarantee that any required inputs will be provided with the correct data type in all API requests.

<table data-full-width="true"><thead><tr><th width="138">Property</th><th width="100">Type</th><th width="108">Required</th><th>Example</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>string</td><td>Yes</td><td>"location"</td><td>The name of the input. When your plugin is activated, the data we send you will use this as the key in the data object (see <a data-mention href="creating-plugins.md#api-request-format">#api-request-format</a>).</td></tr><tr><td>type</td><td>string</td><td>Yes</td><td>"string"</td><td>Can be "string" or "number".</td></tr><tr><td>required</td><td>boolean</td><td>Yes</td><td>true</td><td>Whether the input is required. Inputs that are not required may not be included with an API request.</td></tr><tr><td>description</td><td>string</td><td>Yes</td><td>"The general location on Earth to get the weather for. Can be a country, city, town, or other location identifier."</td><td>A description of the input that describes the value that is expected.</td></tr><tr><td>example</td><td>string / number</td><td>No</td><td>"London"</td><td>An example of a valid input value. Must be a number if the input type is "number", otherwise must be a string. See the note below for why we recommend avoiding examples for most cases.</td></tr></tbody></table>

{% hint style="warning" %}
Adding example values to API inputs can sometimes cause the agent to use the example value instead of asking the user for it. **We recommend avoiding example values in API inputs** unless the system is consistently providing values in the wrong format. Contact us if you believe you are experiencing a bug.
{% endhint %}

### Outputs

The `api.endpoints.outputs` property in the manifest file describes the output values that the endpoint provides. You can have up to 10 inputs per endpoint. The outputs from your API must match those described in the manifest file, otherwise the response will be rejected.

<table data-full-width="true"><thead><tr><th width="138">Property</th><th width="100">Type</th><th width="108">Required</th><th width="264">Example</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>string</td><td>Yes</td><td>"temperature_deg_c"</td><td>The name of the output. You should aim to make this descriptive enough that it can be discerned even without its associated description.</td></tr><tr><td>type</td><td>string</td><td>Yes</td><td>"number"</td><td>Can be "string", "number", or "object".</td></tr><tr><td>description</td><td>string</td><td>Yes</td><td>"The temperature of the location in degrees celcius."</td><td>A description of the value that is provided by the endpoint.</td></tr><tr><td>example</td><td>string / number</td><td>Yes</td><td>"15"</td><td>An example of an output value. Must be a number if the output type is "number", otherwise must be a string. In the case of the output being of type "object", the string should contain a small stringified JSON object.</td></tr></tbody></table>

### Example

Here is an example manifest file that describes Joe's Awesome Weather plugin, with endpoints to get the current weather and current weather warnings.&#x20;

{% code fullWidth="false" %}
```json
{
  "manifest_version": "1",
  "developer_id": "646cd283be483c45b56b3a8f",
  "version": "1.0.0",
  "name": "joes-awesome-weather",
  "name_for_human": "Joe's Awesome Weather",
  "name_for_machine": "weather",
  "description_for_human": "Get up-to-date weather information.",
  "description_for_machine": "Get up-to-date weather information.",
  "author_name": "Joe Bloggs",
  "contact_email": "j.bloggs@example.com",
  "api": {
    "base_url": "https://example.com",
    "endpoints": [
      {
        "name": "get_current",
        "description": "Get the current weather for a location.",
        "path": "/current",
        "method": "POST",
        "input": [
          {
            "name": "location",
            "type": "string",
            "required": true,
            "description": "The general location on Earth to get the weather for. Can be a country, city, town, or other location identifier.",
            "example": "London"
          }
        ],
        "output": [
          {
            "name": "temperature_deg_c",
            "type": "number",
            "description": "The temperature of the location in degrees celcius.",
            "example": 18.5
          },
          {
            "name": "humidity_percent",
            "type": "number",
            "description": "The humidity of the location in percent.",
            "example": 65
          },
          {
            "name": "condition_description",
            "type": "string",
            "description": "A description of the weather condition.",
            "example": "Overcast with showers"
          },
        ]
      },
      {
        "name": "get_weather_warnings",
        "description": "Get weather warnings for a location.",
        "path": "/warnings",
        "method": "POST",
        "input": [
          {
            "name": "location",
            "type": "string",
            "required": true,
            "description": "The general location on Earth to get weather warnings for. Can be a country, city, town, or other location identifier.",
            "example": "London"
          }
        ],
        "output": [
          {
            "name": "weather_warnings",
            "type": "string",
            "description": "A description of the weather warnings for the location.",
            "example": "There are no weather warnings in effect right now."
          }
        ]
      }
    ]
  }
}
```
{% endcode %}

## Creating Your First Plugin

Now that you know what we expect of your API and manifest file, you're ready to create a plugin! We have created a [Replit template](https://replit.com/@CallumAtCarter/Carter-Plugin-Template?v=1) that you can use to get started quickly. It includes basic request and response models, along with a manifest file and "Hello World" API example.

### Instructions

1. Become a developer and retrieve your developer ID: `/plugin dev start`.
2. Create a plugin API and host a manifest file at the root of the API (or higher) with your developer ID and a unique name. If you try to create a plugin with the same name as an existing plugin, you will receive an error and need to choose a different name. Don't worry though, the name property is just so that we can tell plugins apart—the display name property (`name_for_human`) doesn't have to be unique.
3. Submit your plugin manifest to receive a plugin code: `/plugin dev submit https://example.com/carterplugin.json`. Note: At this point, your plugin is still private—only you can see and install it.
4. (Optional) Request your plugin's secret token: `/plugin dev token <code>`. If you're using our Replit template, simply add this code to the `CARTER_PLUGIN_SECRET_TOKEN` environment variable to automatically verify it for all requests. If you're writing your own plugin from scratch, you'll want to read [#secret-token](creating-plugins.md#secret-token "mention") to learn how to use this value.
5. Install your plugin: `/plugin install <code>`. The plugin will only be installed on the single relationship between you and the agent, see [#install-and-use-plugins](../overview.md#install-and-use-plugins "mention").
6. (Optional) Publish your plugin so that others can install it: `/plugin dev publish <code>`. Then, share your plugin code with the community in the [Carter Discord server](https://discord.gg/carter).

### Troubleshooting

* If you're receiving an error when submitting your plugin manifest, it may have invalid content. Validate your manifest's content [here](https://www.jsonschemavalidator.net/s/bUzIujo4).
* If you're trying to install someone else's plugin and you receive an error stating that the plugin could not be found, it may still be private. Let them know that they must publish it before others can install it.

## Updating Your Plugin

After you have submitted a plugin, you might wish to make changes. This could be because the functionality of your API is changing, or because you want to adjust the names, descriptions, and examples for inputs and outputs to improve reliability.

1. Start by making changes to your manifest file. You must keep the `name` and `developer_id` fields the same as these identify the plugin and associate it with your account.
2. Increment your manifest's `version` field, e.g. from "1.0.0" to "1.0.1" (the exact value isn't important).
3. Submit your new manifest: `/plugin dev submit <url>`. Your plugin will automatically update for everyone that has it installed.

## Example Plugin

In [#instructions](creating-plugins.md#instructions "mention") we introduced a [Replit template](https://replit.com/@CallumAtCarter/Carter-Plugin-Template?v=1) that can be used to get started with plugin development quickly. In this section we will discuss a simple example plugin to show how a plugin can be made in practice.

### Random Number Generator

For this example, we will discuss a plugin that provides random number generation functionality to our agents. This plugin was made starting with the aforementioned template.

View the final [Random Number Generator plugin example on Replit](https://replit.com/@CallumAtCarter/Carter-RNG-Plugin-Example?v=1#README.md).

This plugin is be able to:

* simulate the roll of a die to generate a random number between 1 and 6
* generate a random number between any two values

#### The Manifest

Every plugin needs a manifest, and this example is no exception. Let's discuss some of the more pertinent values.

Below we are giving the plugin a name and description that users will see (`for_human`), and that the internal plugin system will see and use to activate your plugin (`for_machine`). In this case, the description for both is the same. This is how we recommend starting with a new plugin unless our system is struggling to understand your plugin, in which case you can add additional context into the `description_for_machine` field.

```json5
"name_for_human": "Random Number Generator",
"name_for_machine": "random_number_generator",
"description_for_human": "Generate random numbers between two values or from a die.",
"description_for_machine": "Generate random numbers between two values or from a die.",
```

Next we will define the endpoints that we're going to provide. In this case we will have two, one for rolling a die and one for a random number between two values. Notice that only the latter has inputs, namely the range start and end values.

```json5
"endpoints": [
  {
    "name": "roll_die",
    "description": "Roll a die to get a number between 1 and 6.",
    "path": "/roll_die",
    "input": [],
    "output": [
      {
        "name": "die_value",
        "type": "number",
        "description": "A random number between 1 and 6.",
        "example": 4
      }
    ]
  },
  {
    "name": "random_number",
    "description": "Generate a random number between two values.",
    "path": "/random_number",
    "input": [
      {
        "name": "from_value",
        "type": "number",
        "required": True,
        "description": "The starting value of the range (inclusive)."
      },
      {
        "name": "to_value",
        "type": "number",
        "required": True,
        "description": "The ending value of the range (inclusive)."
      }
    ],
    "output": [
      {
        "name": "random_number",
        "type": "number",
        "description": "A random number between two values.",
        "example": 4
      }
    ]
  }
]
```

#### The API

Now that we've described the API we'll be making, it's time to actually make it. Here we'll just look at `roll_die`, and you can view `random_number` in the final Replit. The code here is written in Python with FastAPI; it will look different if you make it with a different language or framework.

As you can see, the logic is very simple:

* accept a request with no inputs (line 5)
* calculate a random integer between 1 and 6 (line 7)
* return the value within a standard response with `success = true` (line 9)

{% code lineNumbers="true" %}
```python
@app.post("/api/roll_die",
          response_model=PluginResponse[RollDieResponseData],
          response_model_exclude_none=True)
def roll_die(
  request: PluginRequest[EmptyData]
):
  die_value = random.randint(1, 6)

  return PluginResponse[RollDieResponseData](
    success=True,
    data=RollDieResponseData(die_value=die_value)
  )
```
{% endcode %}

And that's all we need to submit our plugin to Carter using the `/plugin dev submit <url>` command.

If you're struggling with any part of making plugins for Carter, join our [Discord server](https://discord.gg/carter) where our passionate community, along with us, can give you a helping hand. We look forward to seeing your creations!
