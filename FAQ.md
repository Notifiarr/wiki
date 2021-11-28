---
title: Frequently Asked Questions
description: 
published: true
date: 2021-11-28T21:25:10.631Z
tags: 
editor: markdown
dateCreated: 2021-05-25T16:43:06.324Z
---

# Configuration
<br>

## Q. Is the Notifiarr client required?

- The client is only required for certain integrations/features. This means the Media Request integration needs enabled and the connect added. You dont have to use requests but that is where the client connection is saved.

	### Integrations
    1. Channel Stats
    1. Dashboard
    1. Media Request
    1. Network 
    1. Plex 
    1. Snapshot
    1. TRaSH 

  ### Features
    1. Radarr Collections
    1. Automatic ununmonitoring of movies/epsiodes after finish
    1. Automatic plex session killing per user/device based on rules
    1. Stuck queue item notifications

## Q. How do I monitor the queue for stuck items?

Open the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration) on the site and expand the **Starr** section to set the notify times.

It will notify once when it thinks it is stuck and then update the existing message every 5 minutes until it is imported so you can see the amount of time it is stuck and why. Messages go to the shared `Errors` channel.

If you want the notifications to stop coming for a specific item, click the `Acknowledge` link in the notification. This is useful if something has a low amount of peers for example so it could take some time to complete it.

## Q. How do I test/troubleshoot Plex?

### Connection:
You can run a curl command and make sure you get a 200 response returned. 

```curl -I -H "X-Plex-Token: <token>" <url>/status/sessions```

- `<token>` The plex token from your config (ENV or conf file) Ex: `ZQonMnitLFbFsuaLXT9Yj`
- `<url>` The plex URL from your config (ENV or conf file). Ex: `http://localhost:32400`


Expected result: HTTP/1.1 200 OK
Incorrect result: HTTP/1.1 401 Unauthorized

Adjust the token and url until it is 200. Once you have the proper information added, **restart Notifiarr** so it uses the new configuration. If you are not sure how to get the token, find your token: [Plex Forums](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)

### Notifications & Sessions:
If session info is missing from notifications or the sessions notification is not working:

- Make sure you dont have duplicated clients in the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration)
- Make sure you have a [client](https://notifiarr.wiki/en/Website/ClientConfiguration) setup for Plex
- Make sure you have selected the **Activity** checkbox in the Plex section of the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration)
- Try to increase the **Activity Delay** in the Plex section of the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration) as this will give Plex more time to get the session available in the endpoint
- Note 1: The sessions notifications will only send when there is at least one item being played or paused
- Note 2: It doesn't matter what Tautulli shows or the Plex Dashboard shows, they both use the same sessions endpoint. If you where to look at them at the same time as the notification is sent (when it doesn't work) they would also not show the session yet. How long it takes Plex & your (possibly low powered or over worked) server to make the session available in the endpoint is out of our control which is why we added the delay option

## Q. What are the user level differences
- `User` Free for all
	- Access to all integrations and notifications (Except TRaSH sync) 
  - Limited to 12k notifications per day

- `Patron` One time support contribution
	- User access
  - Patron channel access on discord
  - Access to TRaSH CF/RP sync and extra CFs not on the guide
  - Custom plex session management for managing users/devices and killing sessions
  - Limited to 24k notifications per day

- `Subscriber` Monthly/Yearly support contribution
	- Patron access
  - Subscriber channel access on discord
  - Radarr gaps (automated collection monitoring)
  - Custom integration icons
  - Unlimited notifications per day
  - **Note** If you cancel the subscription, you'll be shifted into `Patron`