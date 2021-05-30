---
title: Jellyfin
description: 
published: true
date: 2021-05-30T04:36:25.540Z
tags: 
editor: markdown
dateCreated: 2021-05-22T22:04:40.095Z
---

> This integration allows for notifications from the Jellyfin media app

---

## Trigger options

![trigger-channels.png](/jellyfin/trigger-channels.png)

1. Triggers
    - `Items` - Receive a notification when media is added
    - `Play` - Receive a notification when media has started playing
    - `Stop` - Receive a notification when media has stopped playing
    - `Plugin Install` - Receive a notification when a plugin has been installed
    - `Plugin Uninstall` - Receive a notification when a plugin has been removed
1. More Triggers
    - Open the configuration to enable/disable more triggers
1. Channel
    - Setup all the channels needed for each trigger

---

## Configuration

![open-configuration.png](/jellyfin/open-configuration.png)

Click the **cog icon** to open the configuration options for Jellyfin.

![configuration.png](/jellyfin/configuration.png)

1. Enable triggers and pick colors for each trigger
1. Expand the notification content settings

![configuration-2.png](/jellyfin/configuration-2.png)

1. Notification content options that you can turn on/off to show in the notifications

### Instructions

![instructions.png](/jellyfin/instructions.png)

1. This needs to be done in Jellyfin before webhooks can be used
1. After the webhook plugin is installed, this is how you add the webhook for Notifiarr
