---
title: Sonarr
description: 
published: true
date: 2022-03-11T04:27:52.911Z
tags: 
editor: markdown
dateCreated: 2021-05-22T02:24:43.287Z
---

> This integration allows for notifications from Sonarr using the connect for Webhooks. In Sonarr click Settings → Connect → <kb>+</kb> → Webhook (Note that: the Sonarr Developers refuse to add Notifiarr as a native connection) and the instructions are below on what information to use.
{.is-info}


## Trigger options

![triggers-channels.png](/sonarr/triggers-channels.png)

### 1. Triggers

- `Grab` - Receive a notification when media is initially grabbed (RSS or manual)
- `Download` - Receive a notification when media **new** is successfully imported
- `Update` - Receive a notification when the application updates
- `Upgrade` - Receive a notification when **upgraded** media is successfully imported
- `Failed` - Custom notification type based on previous grabs. If the system detects a grab for the same media with the same quality or better before the previous one was imported then it will set the previous one as failed
- `Health` - Receive a notification when the applicarion reports an issue
- `Backup` - Receive a notification when a backup occurs ([Notifiarr Client Required](/Client/Main))
- `Corrupt` - Monitor backups for corruption and size loss ([Notifiarr Client Required](/Client/Main))
- `Deleted` - Be notified when media is deleted

### 2. Channels

- Sonarr channel picker for each trigger


## Configuration

![open-configuration.png](/sonarr/open-configuration.png)

Click the **cog icon** to open the configuration options for Sonarr.

![configuration.png](/sonarr/configuration.png)

1. Basic instructions on how to add the Notifiarr to Sonarr including the proper URL
1. Trigger options and colors for the notification
1. Custom icon (Subscriber feature)
1. An optional content line added to notifications for mobile/wearable devices

![configuration.png](/sonarr/configuration-2.png)

5. Custom regular expression option to exclude health checks that match
6. Option to only send notifications if corruption detects a warning or error
7. Option to stop notification updating and send a notification for everything
8. Option to delete the grab notification after the import notification is received

![configuration-2.png](/sonarr/configuration-3.png)

1. Notification content options that you can turn on/off to show in the notifications
1. Launch the integration layout editor (image below)

![layout-editor.png](/sonarr/layout-editor.png)

1. Drag and drop positioning of where you want to see each piece of information in the notification. Some fields are locked (red outline). Full width items can not be used in a multi-line layout. You can not have more than 3 items per line.
1. Test Layout - Will send a test notification with the current layout format
1. Save Layout - Will save the current layout format as the one you want to use
1. Reset Layout - Will set the layout back to default

### Instructions

> For the latest instructions - refer to the Instructions within the Integration setting on the site {.is-info}

![layout-editor.png](/sonarr/instructions.png)

1. In Sonarr navigate to Connect => Add New (Plus Button) => Webhook
2. Enter the webhook URL in the URL field
2. Enter a name for the Notification in Sonarr `Notifiarr` is suggested, but use what you like
2. Enable the notification triggers you wish to have sent from Sonarr to the Notifiarr Site
2. Hit test - you should receive a notification on discord with the test message from Sonarr
2. Save
3. Add `?instance=<name-here>` if you want to use multiple instances
4. Send a test notification from the site to your discord server

### Errors

#### 400 Bad Request

- Check and ensure you have a Grab or Download channel configured for Sonarr (Test notifications try to use Grab, then Download to send, you can disable after the test if you want)
- Ensure the webhook URL is accurate

#### 401 Unauthorized

Your APIKey is incorrect