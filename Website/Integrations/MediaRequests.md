---
title: Media Requests
description: 
published: true
date: 2022-03-11T16:32:09.479Z
tags: 
editor: markdown
dateCreated: 2021-05-23T00:33:58.147Z
---

> This integration allows for requesting media via Discord.
{.is-info}

## Currently Supported Applications

- Lidarr
- Radarr (v3+)
- Readarr
- Sonarr (v3+)
  - Note that for most uses involving the Notifiarr Client require Sonarr v3.0.6.1355 or newer

## Trigger options

![triggers.png](/mediarequests/triggers.png)

### Triggers

- `Lidarr`<sup>1</sup> - Enable Lidarr requests for an instance
- `Radarr`<sup>1</sup> - Enable Radarr requests for an instance
- `Readarr`<sup>1</sup> - Enable Readarr requests for an instance
- `Sonarr`<sup>1</sup> - Enable Sonarr requests for an instance

### Channel

- Pick the channel on your server to monitor for requests and send optional approval messages.

---

## Configuration

### Global configuration

![open-configuration.png](/mediarequests/open-configuration.png)

Click the **cog icon** to open the configuration options for *arr apps.

![configuration.png](/mediarequests/configuration.png)

1. The client to use for Media Requests
1. Default \*arr apps, opening them allows for individual configuration. Details below
\+ button adds another instance of an \*arr app. This also needs configured in the Notifiarr client conf (or ENV if you use that) Details below
1. User based granular options
1. Cleanup will remove all the ping/pong messages when adding things, leaving only the final message.
1. Default keywords that control the bot, change them however you want.

### Multiple instances

![configuration-2.png](/mediarequests/configuration-2.png)

1. Add another instance of an \*arr app to be used for anything related to the Notifiarr client.
1. Example conf setup for multiple instances.

### App settings

![app-settings.png](/mediarequests/app-settings.png)

1. Keyword the bot looks for when adding something. add ***movie*** batman for example.
1. Settings used when adding media to \*arr.

### User settings

![user-settings.png](/mediarequests/user-settings.png)

1. Discord users that can be used to assign permissions to
1. User details
1. App settings for the user

### Instructions

![instructions.png](/mediarequests/instructions.png)

A basic overview on how to use the integration. This may change from time to time on the site without updating the screenshot here.
