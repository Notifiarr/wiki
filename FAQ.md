---
title: Frequently Asked Questions
description: 
published: true
date: 2021-06-28T16:13:38.287Z
tags: 
editor: markdown
dateCreated: 2021-05-25T16:43:06.324Z
---

# Configuration
<br>

## Q. Is the Notifiarr client required?

- The client is only required for certain integrations/features.

	### Integrations
    1. Media Request
    1. Network 
    1. Plex 
    1. Snapshot 
    1. TRaSH 

  ### Features
    1. Radarr Collections

## Q. How do I monitor the queue for stuck items?

- Make sure you are using at least v0.1.9 of the Notifiarr client
- Modify the client conf file and add `stuck_items = true` to each \*arr section you want to track

Example:
```
[[radarr]]
  name     = "App: Radarr"
  url      = "http://localhost:7878"
  api_key  = ""
  interval = "5m0s" # service check duration (if name is not empty)
  timeout  = "1m0s"
  stuck_items = true
```

It will notify once when it thinks it is stuck and then update the existing message every 5 minutes until it is imported so you can see the amount of time it is stuck and why. Messages go to the shared `Errors` channel.

## Q. How do I test the Plex connection?

You can run a curl command and make sure you get a 200 response returned. 

```curl -I -H "X-Plex-Token: <token>" <url>/status/sessions```

- `<token>` The plex token from your config (ENV or conf file) Ex: `ZQonMnitLFbFsuaLXT9Yj`
- `<url>` The plex URL from your config (ENV or conf file). Ex: `http://localhost:32400`


Expected result: HTTP/1.1 200 OK
Incorrect result: HTTP/1.1 401 Unauthorized

Adjust the token and url until it is 200. Once you have the proper information added, **restart Notifiarr** so it uses the new configuration. If you are not sure how to get the token, find your token: [Plex Forums](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)