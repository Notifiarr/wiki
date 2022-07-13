---
title: Client Configuration
description: 
published: true
date: 2022-06-04T14:41:27.055Z
tags: 
editor: markdown
dateCreated: 2021-11-14T04:45:07.704Z
---

# Client Configuration

The client is used to do all local communication between the site and your system. This allows all urls, apikeys, etc to stay local and requires apikey validation between the site and the client before any actions can be taken.

Going forward, it will be assumed you have configured the client already and have the port forwarded or the reverse proxy setup properly so the site can communicate with the client.

At the top of the `Integration Setup` page you will find the button to modify the settings for all the clients you have setup

![client-config-button.png](/clientconfig/client-config-button.png)

The dialog for client settings is temporary until a more UX friendly way to manage all these settings is decided.

![client-config-settings-1.png](/clientconfig/client-config-settings-1.png)

1. Client list: Each client you have configured will show up as a tab so its settings can be modified
1. This section is information about the local client and its host environment
1. This is the URL to the client so the site can communicate with it (Not required but if there is not one setup, many features will not work and the sync will be on a poll)

- This cannot be `http://192.168.*.*:5454` - That is a local network IP
- This cannot be `http://10.1.*.*:5454` - That is a local network IP
- This can be `http://<your-external-ip>:5454` - With a port forward to point that port to the local machine IP
- This can be `https://notifiarr.domain.com` or `https://domain.com/notifiarr` if you use a reverse proxy with a port forward to point that port to the local machine IP

1. This is the connection status, if it isn't green then the site can not reach the client. Change the URL accordingly and click the icon to re-test until it turns green
1. Client triggers: If the URL is provided, you can trigger the client to run any of these actions by clicking the cloud icon
1. Bot trigger: If the URL is provided, you can pick a keyword and channel for the bot to monitor and it will give you the option to trigger any of the actions from all available clients
1. Settings: The client needs to know how to handle each integration. Expand each one and configure them accordingly. Make sure the actual integration is enabled as well

![client-config-settings-2.png](/clientconfig/client-config-settings-2.png)

1. Save button: Once done, click this and it will update all your settings. If a URL is provided it will trigger the client to fetch the new settings right then. If no URL is provided then you can restart the client manually to pull the changed settings or wait 5 minutes for the client poller to request any changed settings and update
1. If you have a duplicate client showup (change the user, hostname changed, etc) you can merge the new client with the old one so all the settings copy over and the old one is removed
1. If you no longer have the client installed on a specific hostname, you can remove it

## Duplicate Clients

- This typically occurs in Docker or \*BSD when a [hostname is not configured](/Client/Installation#hostname) everytime the container is restarted.
- For other installations this would occur if the unique attributes of your host system and installation change.

## Resolving Duplicate Clients

1. Configure/Set a hostname for the client if applicable or resolve the changing attributes
1. Restart the client
1. On the Website in Client Configuration, Delete all client entries between the first and last client
1. On the Website in Client Configuration, Merge the remaining two client entries
