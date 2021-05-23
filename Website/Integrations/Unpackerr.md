---
title: Unpackerr
description: 
published: true
date: 2021-05-23T02:26:42.821Z
tags: 
editor: markdown
dateCreated: 2021-05-23T02:26:42.821Z
---

> This integration allows for notifications from Unpackerr.

Reaction example:

![reaction.png](/unpackerr/reaction.png)

---

## Trigger options

![trigger-channels.png](/unpackerr/trigger-channels.png)

1. Triggers
    - `Processing` - Be notified when Unpackerr has started processing (Extracting, Extracted)
    - `Imported` - Be notified when Unpackerr as marked it imported
    - `Failed` - Be notified of when Unpackerr fails to unpack
    - `Update Available` - Not part of Unpackerr, this is a check Notifiarr does 
1. Channel
    - Which channel to send Unpackerr notifications to

---

## Configuration

![open-configuration.png](/unpackerr/open-configuration.png)

Click the **cog icon** to open the configuration options for Unpackerr.

![configuration.png](/unpackerr/configuration.png)

1. Pick the colors for notification triggers
1. Add a reaction to the grab/download from \*arr 

### Instructions

![instructions.png](/unpackerr/instructions.png)

- How to add the webhook to the Unpackerr conf file