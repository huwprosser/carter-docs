---
description: A brand new API for the next chapter of personal intelligence...
---

# Unstable API

Welcome to the Unstable API documentation! We are excited to introduce our next-generation API, which provides enhanced memory and powerful tools for developers. Please note that while this API is currently labeled as "unstable," it is the future of our platform, and we encourage you to start transitioning from the existing Carter API to the Unstable API for all non-production projects. This documentation will guide you through the changes and provide instructions on how to make the switch.

### New API. New toys

We've packed in new functionality at launch and have a few things rolling out over the next few weeks that will let you build incredible applications with Carter. Most notably we've added:

* Cross-platform relationships. Allowing users to persist the same relationship with your Agent across devices and experiences. We will warm up to this in the coming weeks!
* Improved memory. Agents can now remember things in much more detail and use them to really personalise your user's experience more and more over time.

<mark style="color:blue;">**LAUNCHING SOON:**</mark>

* New endpoints! Keep your eyes peeled as we announce these.
* Plugins v2 - powerful new ways to extend Agents in every way you can imagine.

You can find our entire current API spec [here](https://unstable.carterlabs.ai/docs).

### Transitioning to the Unstable API

To switch from the existing Carter API to the Unstable API, follow these steps:

1. **Update API Endpoint**: Update your API endpoint URL from `https://api.carterlabs.ai` to `https://unstable.carterlabs.ai/api` in your application code.
2. **Replace Player IDs with User IDs**: Throughout your codebase, search for instances where Player IDs are used and replace them with User IDs. This ensures compatibility with the Unstable API's updated terminology.&#x20;

```json
// an example of the new request format
{
    "text": "[YOUR MESSAGE TO CARTER]",
    "key": "[YOUR API KEY]",
    "user_id": "[UNIQUE USER ID]",
}
```

<mark style="color:red;">**USER IDs MUST BE UNIQUE WITHIN YOUR APPLICATION. DO NOT USE NAMES ETC.**</mark>

### Feedback and Support

We value your feedback during this transition period. If you encounter any issues, have questions, or need further assistance, please reach out to us on Discord!
