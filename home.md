---
title: About
description: 
published: true
date: 2022-06-12T00:40:16.760Z
tags: 
editor: markdown
dateCreated: 2021-05-22T00:58:35.895Z
---

# Notifiarr

This is not something we are trying to get hundreds of thousands of users using, so you wont see it being announced or advertised. Use  NotifiRr if it is helpful, don't if it isn't! The information in the wiki is more of a quick high level overview and you can visit the site for full details or hop on Discord.

## Support

[![Discord chat](https://img.shields.io/discord/764440599066574859?style=plastic&color=blue&logo=discord)](https://discord.gg/AURf8Yz)

## Website

![GitHub issues](https://img.shields.io/github/issues/Notifiarr/website?color=blue&logo=github&style=plastic) ![GitHub issues](https://img.shields.io/github/issues-closed/Notifiarr/website?color=blue&logo=github&style=plastic)

## Notifiarr Client

![GitHub issues](https://img.shields.io/github/issues/Notifiarr/notifiarr?color=blue&logo=github&style=plastic) ![GitHub issues](https://img.shields.io/github/issues-closed/Notifiarr/notifiarr?color=blue&logo=github&style=plastic)  ![GitHub issues](https://img.shields.io/github/issues-pr/Notifiarr/notifiarr?color=blue&logo=github&style=plastic)  ![GitHub issues](https://img.shields.io/github/issues-pr-closed/Notifiarr/notifiarr?color=blue&logo=github&style=plastic) [![GitHub license](https://img.shields.io/github/license/Notifiarr/notifiarr?color=blue)](https://github.com/Notifiarr/notifiarr/blob/main/LICENSE)

## Wiki

![GitHub issues](https://img.shields.io/github/issues/Notifiarr/wiki?color=blue&logo=github&style=plastic) ![GitHub issues](https://img.shields.io/github/issues-closed/Notifiarr/wiki?color=blue&logo=github&style=plastic)  ![GitHub issues](https://img.shields.io/github/issues-pr/Notifiarr/wiki?color=blue&logo=github&style=plastic)  ![GitHub issues](https://img.shields.io/github/issues-pr-closed/Notifiarr/wiki?color=blue&logo=github&style=plastic)

## Notifiarr Purpose

This was built about 2 years ago for [me](https://github.com/austinwbest) and used by only me locally until about August of 2020 when I opened it up for others to use. My goal has always been to have a single location for common notification needs, so I am not jumping around 20 apps to do things.

## Integrations

### \*Arr

* [Lidarr](/Website/Integrations/Lidarr.md)
* [Radarr](/Website/Integrations/Radarr.md)
* [Readarr](/Website/Integrations/Readarr.md)
* [Sonarr](/Website/Integrations/Sonarr.md)
* [Prowlarr](/Website/Integrations/Prowlarr.md)
{.links-list}

### \*Arr Companions

* [Release Parser](/Website/Integrations/ReleaseParser.md)
* [Bazarr](/Website/Integrations/Bazarr.md)
* [Unpackerr](/Website/Integrations/Unpackerr.md)
{.links-list}

### Media Requests

Note that the Notifiarr Client is required for Media Requests

* [Lidarr](/Website/Integrations/MediaRequests.md)
* [Radarr](/Website/Integrations/MediaRequests.md)
* [Readarr](/Website/Integrations/MediaRequests.md)
* [Sonarr](/Website/Integrations/MediaRequests.md)
{.links-list}

### Media Management

* [Emby](/Website/Integrations/Emby.md)
* [Jellyfin](/Website/Integrations/Jellyfin.md)
* [Plex](/Website/Integrations/Plex.md)
* [Plex Meta Manager](Website/Integrations/PMM.md)
{.links-list}

### Network

* [Process & Application Monitoring](/Website/Integrations/Network.md)
* [System Snapshots](/Website/Integrations/Snapshots.md)
{.links-list}

### Websites

* [Better Uptime](/Website/Integrations/BetterUptime.md)
* [Website Monitoring](/Website/Integrations/WebsiteStatus.md)
{.links-list}

### Misc

* [Github](/Website/Integrations/Github.md)
* [Reddit Subreddit](/Website/Integrations/Reddit.md)
* [Hotio: Pullio](/Website/Integrations/Hotio.md)
* [TRaSH: Sync *Patron*](/Website/Integrations/Trash.md)
{.links-list}

## Additional Features

* Fully configurable on what triggers to get notifications for. Each integration and many triggers in them can go to their own channels.
* Layout configuration for some notifications
* Content configuration for most notifications (color, content, etc)
* Media Requests Bot - Discord Bot for all 4 \*Arr apps with:
  * Media Requests
  * User Permissions
  * Approvals
  * Sonarr Profiles
  * Default Options
  * Series Following
  * Discover features
  * Multi-Instance Support
* Minimal Access - Only port open that is needed is for the client to communicate with the site. No \*Arr apikeys or anything of the sort is used or saved on the site. All requests to the client are verified with your Notifiarr apikey and thrown out if they don't match up
* TRaSH Custom Format Sync [*\*Patron Feature\**](/FAQ#q-what-are-the-user-level-differences) - Automated continuous add/sync for the custom formats TRaSH has made to use with Radarr
* Radarr Collections - A fully automated way to monitor all your Radarr collections with auto add new items to your library as they are put into the collection on TMDb for any monitored collections, etc.
