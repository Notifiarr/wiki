---
title: Plex
description: 
published: true
date: 2021-05-23T04:11:43.932Z
tags: 
editor: markdown
dateCreated: 2021-05-23T04:11:41.340Z
---

> This integration allows for notifications from Plex. Keep in mind this utilizes the Notifiarr client so you will need to enable the Media Requests integration and set it up (even if you dont want to request media)

Reaction example:

![reaction.png](/plex/reaction.png)

## Trigger options

![trigger-channels.png](/plex/trigger-channels.png)

1. Triggers
    - `Play` - Notify when a user starts playing media
    - `Resume` - Notify when a user resumes playing media
    - `Finished` - Notify when a user finishes playing media
    - `Sessions` - Get notifications about streaming sessions and minimal server information
    - `Devices` - Notify when a new device is added
    - `Backup` - Notify when a backup was completed
    - `Corruption` - Notify when database corruption is detected
1. Channel
    - Channel(s) to use for sending plex notifications

## Configuration

![open-configuration.png](/plex/open-configuration.png)

Click the **cog icon** to open the configuration options for Plex.

![configuration.png](/plex/configuration.png)

1. Notification style setting
1. Notification triggers
1. Notification colors
1. Notification options
1. Content lines are small previews of the full notification for toast/push notifications

![configuration-2.png](/plex/configuration-2.png)

1. Table of all users and devices. Uncheck the notify box to not receive notifications from the specific user/device. Kill will open another window with options on killing sessions for the user/device automatically based on rules.
1. Keyword for having the bot display what is currently streaming on your server.
1. Option to be notified whenever a session is automatically killed.

![configuration-3.png](/plex/configuration-3.png)

1. Kill all sessions from a given user/device (Maybe a user shared their login with someone else)
1. Kill the session after a certain amount of consecutive episode plays (Maybe a user has fell asleep)
1. Kill all sessions on specific days and between certain times

### Instructions

![instructions.png](/plex/instructions.png)

1. Basic instructions on how to setup the Notifiarr conf file to work with Plex notifications
