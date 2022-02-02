---
title: API Errors
description: 
published: true
date: 2022-02-02T03:47:09.185Z
tags: 
editor: markdown
dateCreated: 2022-02-02T03:47:09.185Z
---

# API Error Help

## 5**
Cloudflare issues, try again and it will go away

## 401
You have an invalid apikey. 
- Check that when you copy and pasted it you did not copy extra spaces
- Make sure you do not have an ENV variable set that is incorrect since that overrides the conf file
- Make sure if it is an integration specific key that it is the correct integration you are using it for

## 400

### network integration disabled

If you see this in your log file, it means you have something in the local notifiarr.conf file that is trying to send a service check but you do not have the integration enabled. Your options are:

1. You can ignore the 400 error if you dont want to be told when things are offline
1. You can enable the network integration and mute the channel if you want to rid the 400 but still dont care to know when things are down
1. You can remove the names in the notifiarr.conf and it wont enable the timers
