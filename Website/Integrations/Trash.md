---
title: TRaSH Sync
description: 
published: true
date: 2021-12-30T02:07:32.618Z
tags: 
editor: markdown
dateCreated: 2021-05-23T03:24:50.933Z
---

> This integration allows for keeping aspects of Radarr and Sonarr in sync based on the TRaSH guides. Keep in mind this utilizes the Notifiarr client so you will need to enable the Media Requests integration and set it up (even if you dont want to request media)

## Trigger options

![trigger-channels.png](/trash/trigger-channels.png)

1. Sync
    - The amount of CF's you have in sync
1. Channel
    - Which channel to send TRaSH update notifications to (when TRaSH updates them, removes them, when you sync them or unsync them)


## Configuration

![open-configuration.png](/trash/open-configuration.png)

Click the **cog icon** to open the configuration options for TRaSH.

![configuration-2.png](/trash/configuration-2.png)

1. Enable sync for individual custom formats
1. Enable sync for scores based on your quality profiles

### Custom Formats

![configuration.png](/trash/configuration.png)

1. CF table, click on the CF and it will jump to it
1. CF name, is per TRaSH guides
1. JSON accordion, click to view the raw JSON for the CF
1. Toggle
	- Each instance will have its own toggle <sup>1</sup>
	- Green means it matched an existing CF in your Radarr instance, you can mouseover and it will show you the name as it appears in Radarr. You can name the CF or the fields in each CF anything you want and it will stay in sync

### Custom Format Scores

![configuration.png-3](/trash/configuration-3.png)

1. List of quality profiles from your Radarr instance
1. List of custom formats you can sync the scores for per profile. It is done this way to allow you to have full control over each profile and custom format scores instead of forcing a score to apply to all profiles
1. Sync/Unsync all custom formats for the quality profile
- The custom format must be in sync in order to sync the score

### Notes

1. Currently you need to enable Media Requests integration if you are using multiple instances. Once you enable it you will see a drop down to pick the client, pick the one that has the arr apps configured if you use more than one. Save that and re-open the integration (yes i know this is annoying and it is on the list to fix on [Github](https://github.com/Notifiarr/website/issues/79)) so the 4 buttons on the right show **Online** under whichever you have configured. Click the **+** to the right of the buttons to add another instance. Each instance should already be configured in the client conf file locally. Before you bitch at me, yes i know this is not necessary. This is old code that has not been updated yet and is already on the list on [Github](https://github.com/Notifiarr/website/issues/72). Once you have the extra instances added, reload the site and you will see them in the TRaSH integration.