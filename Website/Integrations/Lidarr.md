---
title: Lidarr
description: 
published: true
date: 2021-05-22T02:27:02.620Z
tags: 
editor: markdown
dateCreated: 2021-05-22T02:00:42.791Z
---

> This integration allows for notifications from Lidarr using its built in Connection for **Notifiarr**

---

## Trigger options

![triggers-channels.png](/lidarr/triggers-channels.png)

1. Triggers
    - `Grab` - Receive a notification when media is initially grabbed (RSS or manual)
    - `Download` - Receive a notification when media **new** is successfully imported
    - `Upgrade` - Receive a notification when **upgraded** media is successfully imported
    - `Health` - Receive a notification when Lidarr reports an issue
1. Channel
    - Lidarr shares the *arr channel unless Granular Setup is used, clicking the link on the site will move to the channel setup location.

---

## Configuration

![open-configuration.png](/lidarr/open-configuration.png)

Click the **cog icon** to open the configuration options for Lidarr.

![configuration.png](/lidarr/configuration.png)

1. Open integration specific instructions
1. Notification colors for each trigger type
1. Unique notifications: Generate a new notification each time (By default notifications edit the previous one so there is a Grab and then the Download ot Upgrade will edit the Grab notification to alleviate the notification spam)

![configuration-2.png](/lidarr/configuration-2.png)

1. Open integration specific instructions
1. Notification content options that you can turn on/off to show in the notifications
1. Launch the integration layout editor (image below)

![layout-editor.png](/lidarr/layout-editor.png)

1. Drag and drop positioning of where you want to see each piece of information in the notification. Some fields are locked (red outline). Full width items can not be used in a multi-line layout. You can not have more than 3 items per line.
1. Test Layout - Will send a test notification with the current layout format
1. Save Layout - Will save the current layout format as the one you want to use
1. Reset Layout - Will set the layout back to default

### Instructions

![instructions.png](/lidarr/instructions.png)

1. How to enable notifications from within Lidarr
1. Test the notification from Notifiarr to Discord
    - This will ensure your server, channel and permissions are set properly in Discord.
