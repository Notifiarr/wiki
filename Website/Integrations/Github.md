---
title: Github
description: 
published: true
date: 2021-05-22T22:46:06.121Z
tags: 
editor: markdown
dateCreated: 2021-05-22T22:46:02.226Z
---

> This integration allows for notifications from public Github repositories.


## Trigger options

![trigger-channels.png](/github/trigger-channels.png)

1. Triggers
    - List of all repositories with notifications enabled

---

## Configuration

![open-configuration.png](/github/open-configuration.png)

Click the **cog icon** to open the configuration options for Github.

![configuration.png](/github/configuration.png)

1. Add the organization URL. You have to be able to manage the selected Organization so you can add webhooks.
1. Remove an existing organization, keep in mind this removes all repositories linked to it
1. Add a discord server. The default server is available but this allows you to push notifications to other servers (example my personal discord (default) or Notifiarr discord).
1. Remove a discord server.
1. Pick a repository, they are pulled automatically based on the organizations added.
1. Copy the `Server` or `Channel` selection to all triggers
1. Available Github triggers

### Instructions

![instructions.png](/github/instructions.png)

This is how you add the webhook to Github and then how you add the organization in the Github integration