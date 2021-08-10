---
title: Readarr
description: 
published: true
date: 2021-05-26T03:03:02.664Z
tags: 
editor: markdown
dateCreated: 2021-05-23T03:12:13.099Z
---

> This integration allows for notifications from Readarr using its built in Connection for **Notifiarr**. In Readarr click Settings → Connect → + → Notifiarr

---

## Trigger options

![trigger-channels.png](/readarr/trigger-channels.png)

1. Triggers
    - `Grab` - Receive a notification when media is initially grabbed (RSS or manual)
    - `Download` - Receive a notification when media **new** is successfully imported
    - `Upgrade` - Receive a notification when **upgraded** media is successfully imported
    - `Health` - Receive a notification when Readarr reports an issue
1. Channel
    - Readarr shares the \*arr channel unless Granular Setup is used, clicking the link on the site will move to the channel setup location.

---

## Configuration

![open-configuration.png](/readarr/open-configuration.png)

Click the **cog icon** to open the configuration options for Readarr.

![configuration.png](/readarr/configuration.png)

1. Enable and colors for each trigger type
1. Trigger specific options
1. Content lines are small previews of the full notification for toast/push notifications
1. 1:1 notifications means each notification will be sent, nothing updates existing messages

![configuration-2.png](/readarr/configuration-2.png)

1. Notification content options that you can turn on/off to show in the notifications
1. Launch the integration layout editor (image below)

![layout-editor.png](/readarr/layout-editor.png)

1. Drag and drop positioning of where you want to see each piece of information in the notification. Some fields are locked (red outline). Full width items can not be used in a multi-line layout. You can not have more than 3 items per line.
1. Test Layout - Will send a test notification with the current layout format
1. Save Layout - Will save the current layout format as the one you want to use
1. Reset Layout - Will set the layout back to default

### Instructions

![instructions.png](/readarr/instructions.png)

1. How to enable notifications from within Readarr
1. Test the notification from Notifiarr to Discord
    - This will ensure your server, channel and permissions are set properly in Discord.
