---
title: Frequently Asked Questions
description: 
published: true
date: 2022-07-28T00:30:09.412Z
tags: 
editor: markdown
dateCreated: 2021-05-25T16:43:06.324Z
---

# Configuration

## Q. Is the Notifiarr client required?

- The client is only required for certain integrations/features. If you open the `Manage Integrations` on the site, it will display in the bottom right corner as well which need the client.

### Integrations

- Channel Stats
- Dashboard
- MDBList (Adding lists & movies to Radarr, Adding shows to Sonarr)
- Media Requests
- Network
- Plex
- Lidarr (Backup, Corruption & Stuck Queue notifications)
- Prowlarr (Backup, Corruption & Stuck Queue notifications)
- Radarr (Backup, Corruption & Stuck Queue notifications)
- Readarr (Backup, Corruption & Stuck Queue notifications)
- Reciperr (Adding lists & movies to Radarr)
- Snapshot
- Sonarr (Backup, Corruption & Stuck Queue notifications)
- TRaSH Custom Format & Profile Sync (Patron)
- Client Commands (\*Coming Soon\*)
  - Discord triggering and advanced features (Sub)

### Features

- Radarr Collections
- Automatic unmonitoring of movies/episodes after finish
- Automatic refresh of TBA episodes
- Automatic plex session killing per user/device based on rules
- Stuck queue item notifications
- Starr backup/corruption check notifications

## Q. How do I monitor the queue for stuck items?

- Open the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration) on the site and expand the **Starr** section to set the notify times.

- It will notify once when it thinks it is stuck and then update the existing message every 5 minutes until it is imported so you can see the amount of time it is stuck and why. Messages go to the shared `Errors` channel.

- If you want the notifications to stop coming for a specific item, click the `Acknowledge` link in the notification. This is useful if something has a low amount of peers for example so it could take some time to complete it.

## Q. How do I test/troubleshoot Plex?

### Locating the Plex Token

- [See this post in the Plex Forums](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)

> The Plex Token is required for the Notifiarr Client to send commands to Plex {.is-info}

### Connection

- You can run a curl command and make sure you get an `200 OK` response returned.

```bash
curl -I -H "X-Plex-Token: <token>" <url>/status/sessions
```

- `<token>` The plex token from your config (ENV or conf file) Ex: `ZQonMnitLFbFsuaLXT9Yj`
- `<url>` The plex URL from your config (ENV or conf file). Ex: `http://localhost:32400`

  - Expected result: HTTP/1.1 200 OK
  - Incorrect result: HTTP/1.1 401 Unauthorized

- Adjust the token and url until it is 200.
- Update the Notifiarr Client's configuration with the correct url and token
- Restart the Notifiarr Client

### Notifications & Sessions

If session info is missing from notifications or the sessions notification is not working:

- Make sure you dont have duplicated clients in the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration)
- Make sure you have a [client](https://notifiarr.wiki/en/Website/ClientConfiguration) setup for Plex
- Make sure you have selected the **Activity** checkbox in the Plex section of the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration)
- Try to increase the **Activity Delay** in the Plex section of the [Client Settings](https://notifiarr.wiki/en/Website/ClientConfiguration) as this will give Plex more time to get the session available in the endpoint
- Note 1: The sessions notifications will only send when there is at least one item being played or paused
- Note 2: It doesn't matter what Tautulli shows or the Plex Dashboard shows, they both use the same sessions endpoint. If you where to look at them at the same time as the notification is sent (when it doesn't work) they would also not show the session yet. How long it takes Plex & your (possibly low powered or over worked) server to make the session available in the endpoint is out of our control which is why we added the delay option

## Q. What are the user level differences

### User

- Cost: Free
- Access to all integrations and notifications (Except TRaSH sync)
- Limited to 12,000 notifications per day

### Patron

- Cost: One time support contribution
- Patron channel access on discord
- Access to TRaSH Custom Format and Release Profile Sync and extra Custom Formats not on the public guide
- Custom Plex session management for managing users/devices and killing sessions
- Limited to 24,000 notifications per day

### Subscriber

- Cost: Monthly or Yearly support contribution
  - **Note** If you cancel your subscription, you'll be shifted into `Patron`
- Patron Access
- Subscriber channel access on discord
- Radarr Gaps (automated collection monitoring)
- Clients Commands via Discord (\*Coming Soon\*)
- Custom Integration Icons
- BYOB (Bring your own bot; you can use your own bot which will be hosted by Notifiarr)
- Unlimited notifications per day

## Q. How to allow Notifiarr through Cloudflare

### WAF Rule

> Free accounts can create 5 Firewall rules
{.is-info}

1. Login to your Cloudflare account and open the domain
1. Click **Security** and then **WAF**
![cf-waf.png](/cloudflare/cf-waf.png)
1. In the WAF section add a new rule by clicking on **Create Firewall Rule**
![cf-waf-firewall.png](/cloudflare/cf-waf-firewall.png)
1. Fill in the rule information

- `Name`: Notifiarr

- `Field`: User Agent
- `Operator`: Equals
- `Value`: Notifiarr
- `Action`: Allow
![cf-waf-firewall-rule.png](/cloudflare/cf-waf-firewall-rule.png)

5. Save the firewall changes

### Cloudflare Tunnel

> This assumes that you already have a Cloudflare tunnel set up on your system. If you want to get started with cloudflare tunnels follow this guide first: <https://www.youtube.com/watch?v=RUJy9fjoiy4>
{.is-info}

1. Login to your Cloudflare teams account at <https://dash.teams.cloudflare.com/>
1. Click **Tunnels** and then **configure** next to the cloudflare tunnel you would like to use
![cf-tunnel-configure_sm2.png](/faq/cf-tunnel-configure_sm2.png)
1. In your Tunnel section click on **Public Hostname** and add a new hostname by clicking on **Add a public hostname**
![cf-tunnel-configure_publichostname.png](/faq/cf-tunnel-configure_publichostname.png)
1. Fill in the public hostname information

- `Subdomain`: Notifiarr (or whatever else you want it to be)

- `Domain`: choose one of your domains
- `Service`: HTTP + Your Local IP Address for Notifiarr
![cf-tunnel-configure_hostnamepage.png](/faq/cf-tunnel-configure_hostnamepage.png)

5. Save Hostname
6. Enter "notifiarr.YourDomain.com" into your Notifiarr Client Settings
![notifiarrclientsettings.png](/faq/notifiarrclientsettings.png)

That's it! The Notifiarr service will now connect to your local server via a cloudflare tunnel.

### OPTIONAL: Increased Security

If you want to increase the security of your local server follow these steps to only allow the Notifiarr service access to your "notifiarr.yourdomain.com" subdomain. There are to steps to this.

#### 1. Limit Access To All Subdomains

1. Login to your Cloudflare teams account at <https://dash.teams.cloudflare.com/>
1. Click on **Applications** and then **Add an application**
![cf-tunnel-addaplication.png](/faq/cf-tunnel-addaplication.png)
1. Select Self-hosted
1. Fill in the Application Configuration information

- `Application Name`: Whatever you want. I usually call this "Domain Catch All"

- `Session Duration`: Whatever you want. I usually choose "1 month" so I don't have to re-authorize very often.
- `Subdomain`: * (that will ensure that this application rule will apply to ALL subdomains on this domain)
- `Domain`: select your domain
![cf-tunnel-catchall.png](/faq/cf-tunnel-catchall.png)

5. Turn on "Skip identity provider selection if only one is configured" at the bottom of the page and click **next**.
![cf-tunnel-instauth.png](/faq/cf-tunnel-instauth.png)
6. Fill in the following Policy information

- `Policy Name`: Whatever you want. I usually call this "Email"

- `Rule Action`: Select **Allow**
- `Configuration Rule Selector`: select **emails**
- `Configuration Rule Value`: enter your personal email address
![cf-tunnel-configure-email.png](/faq/cf-tunnel-configure-email.png)

7. Click **next**
8. On the next page don't make any changes and click **Add Application**

Now when you're trying to access ANY of your cloudflare tunnel subdomains you first have to authorize yourself (via email, once a month) before you can access them:
![cf-tunnel-accesscheck.png](/faq/cf-tunnel-accesscheck.png)

This works very well for your services such as Radarr and Sonarr, for example. Obviously the Notifiarr service won't be able to verify itself via email so we need to make an exception for Notifiarr next.

#### 2. Give Access To Notifiarr Service

1. Login to your Cloudflare teams account at <https://dash.teams.cloudflare.com/>
1. Click on **Applications** and then **Add an application**
![cf-tunnel-addaplication.png](/faq/cf-tunnel-addaplication.png)
1. Select Self-hosted
1. Fill in the Application Configuration information

- `Application Name`: Whatever you want. I usually call this "Domain Notifiarr Bypass"

- `Session Duration`: Whatever you want.
- `Subdomain`: notifiarr
- `Domain`: select your domain
![cf-tunnel-appbypass.png](/faq/cf-tunnel-appbypass.png)

5. Turn on "Skip identity provider selection if only one is configured" at the bottom of the page and click **next**.
![cf-tunnel-instauth.png](/faq/cf-tunnel-instauth.png)
1. Fill in the following Policy information

- `Policy Name`: Whatever you want. I usually call this "Allow I
- `Rule Action`: Select **Bypass**
- `Configuration Rule Selector`: select **IP ranges**
- `Configuration Rule Value`: enter "68.169.163.71". This is the static IP of the Notifiarr service
![cf-tunnel-configure_ip.png](/faq/cf-tunnel-configure_ip.png)

7. Click **next**
8. On the next page don't make any changes and click **Add Application**

That's it! You now gave one specific IP address (Notifiarr service) permission to BYPASS the cloudflare email authorization check. Only the Notifiarr service will have access to "notifiarr.yourdomain.com". (You will still have access to it as well via email authorization).
