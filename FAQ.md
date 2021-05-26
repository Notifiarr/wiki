---
title: Frequently Asked Questions
description: 
published: true
date: 2021-05-26T13:08:48.064Z
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
    
## Q. How do I test the Plex connection?

You can run a curl command and make sure you get a 200 response returned. 

```curl -I -H "X-Plex-Token: <token>" <url>/status/sessions```

- `<token>` The plex token from your config (ENV or conf file) Ex: `ZQonMnitLFbFsuaLXT9Yj`
- `<url>` The plex URL from your config (ENV or conf file). Ex: `http://localhost:32400`


Expected result: HTTP/1.1 200 OK
Incorrect result: HTTP/1.1 401 Unauthorized

Adjust the token and url until it is 200. Once you have the proper information added, **restart Notifiarr** so it uses the new configuration.