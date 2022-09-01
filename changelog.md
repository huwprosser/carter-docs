---
description: Additions and updates to the Carter platform and API.
---

# Changelog

### **August 20th, 2022**

0.0.7

![](<.gitbook/assets/meet lari. (1).png>)

Two words - Screen. Space. We've introduced a new dashboard design, allowing for more efficient use of those ever-more-important pixels. \
\
**Light Theme** "never! I'll ever turn to the dark side!". For those stubborn people with strong retinas, you can now enable light theme of the portal for a breezy, positive vibe when you visit the dashboard.

**Bug Fixes** some users reported on Discord that they were having trouble typing in certain boxes. This should now be fixed.

**Improved Trigger Metadata editor.** Not much else to say here.&#x20;

### **August 17th, 2022**

0.0.6

Based on our awesome Discord Community's feedback, we're pleased to announce another round of new features to ensure you are building on solid foundations.

**Trigger Confidence Removed.** There is no longer a global confidence threshold that applies to every trigger.&#x20;

**Trigger-level sensitivity added.** Set the how confident you want your agent to be, for a **specific** trigger, before triggering a custom trigger. This can be found in the trigger editor.

**Trigger Metadata** attach application data to each custom trigger, reducing demand for client-side logic and load on your database. See how to access this from your agent's response [here](carter-api/api-response.md).

![](<.gitbook/assets/Screenshot 2022-08-17 at 13.11.17.png>)



### **August 11th, 2022**

0.0.5

**Token Limit Removed!** \
****For now, we've completely removed token limits for hobby agents, allowing developers to now get creative and build something awesome without limitations. Developers moving their agent to production will need to upgrade to an enterprise plan for faster inference and better support, to get started with this you can contact us via danny@carterapi.com.

**Named Entity Recognition (NER)** is now available in the API Beta. This allows for the detection of names, locations, organisations etc for each message sent to a Carter agent. Access this via 'entities' within your agent's response.

**Knowledge Confidence Threshold Lowered** allowing agents to more-often answer domain-specific questions from the given knowledge-base.

**1000 Word Limit** per message introduced to prevent API abuse.

**Delete Agents** a simple but highly requested feature. This is irreversible.
