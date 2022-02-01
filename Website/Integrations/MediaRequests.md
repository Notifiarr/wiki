---
title: MediaRequests
description: 
published: true
date: 2022-02-01T14:52:50.071Z
tags: 
editor: markdown
dateCreated: 2021-05-23T00:33:58.147Z
---

> This integration allows for requesting media via Discord.


## Currently supported

- Lidarr
- Radarr (>= v3)
- Readarr
- Sonarr (>= v3)

## Trigger options

![trigger-channels.png](/mediarequests/trigger-channels.png)

1. Triggers
    - `Lidarr`<sup>1</sup> - Enable Lidarr requests for an instance
    - `Radarr`<sup>1</sup> - Enable Radarr requests for an instance
    - `Readarr`<sup>1</sup> - Enable Readarr requests for an instance
    - `Sonarr`<sup>1</sup> - Enable Sonarr requests for an instance
1. Channel
    - Pick the channel on your server to monitor for requests and send optional approval messages.

---

## Configuration

### Global configuration

![open-configuration.png](/mediarequests/open-configuration.png)

Click the **cog icon** to open the configuration options for *arr apps.

![configuration.png](/mediarequests/configuration.png)

1. The URL to connect to the Notifiarr client, when the icon is green the connection is successful.
1. Connection icon is green for a successful connection or orange if it has failed. You can click the icon to retry the connection while setting it up.
1. Default \*arr apps, opening them allows for individual configuration. Details below
1. \+ button adds another instance of an \*arr app. This also needs configured in the Notifiarr client conf (or ENV if you use that) Details below
1. Cleanup will remove all the ping/pong messages when adding things, leaving only the final message.
1. Default keywords that control the bot, change them however you want.
1. (Not Pictured) Request Filled changes the message to the user when a request is filled and downloaded by \*Arr. The default is "Good news!`

### Multiple instances

![configuration-2.png](/mediarequests/configuration-2.png)

1. Add another instance of an \*arr app to be used for anything related to the Notifiarr client.
1. Example conf setup for multiple instances.

### App settings

![configuration-3.png](/mediarequests/configuration-3.png)

1. Keyword the bot looks for when adding something. add ***movie*** batman for example.
1. Settings used when adding media to \*arr.
1. Bot results when searching, how many to show and wwether or not to show a description with each result.
1. Configure individual discord user settings. Details below

### User settings

![configuration-4.png](/mediarequests/configuration-4.png)

- Existing users that have been setup, pick one to modify their settings
- Discord users that can be used to assign permissions to
- If a user can make requests with this \*arr
- If a user needs to have their requests approved
- If a user is allowed to move media around to different root folders
- If a user can approve requests (Note: This trumps requiring approval)

### Instructions

![instructions.png](/mediarequests/instructions.png)

A basic overview on how to use the integration. This may change from time to time on the site without updating the screenshot here.