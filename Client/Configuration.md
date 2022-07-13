---
title: Configuration
description: 
published: true
date: 2022-04-19T22:37:00.732Z
tags: 
editor: markdown
dateCreated: 2021-05-22T01:09:34.150Z
---

# Setup

## Troubleshooting

- Find help on Discord: [Notifiarr](https://discord.gg/AURf8Yz) or [GoLift](https://golift.io/discord)

## Notifiarr Website

There are many settings, timers, options, etc for this and are configured on the Notifiarr site in the `Notifiarr Client Configuration` popup (button is located at the top of the setup page and can configure all clients settings that are related to the site from there). You can get some insight about that [on the wiki](https://notifiarr.wiki/en/Website/ClientConfiguration) as well.

There are core items that the client needs to be able to run and that is explained below.

## Web UI

Open the conf file, OS locations are listed on the Installation page, and find `ui_password = ""` or it might already have a default value in it. Set this to `ui_password="username-here:some-password-here"` and make sure if the line started with a `#` that you remove it. Save and close the file with the `ui_password` configured and then point your browser to the client. This can be something like:

- `http://locahost:5454`
- `http://notifiarr`
- `http://192.168.1.10:5454`

Use the username and password you setup in the conf file to login to the app. Now you can configure and setup the client via the UI. Everything below this (except for the Reverse Proxy information at the bottom) is for those who do not use the UI to change their settings.

## .conf File

- You can use env variables but the conf is suggested
- Must provide an API key from notifiarr.com.
  - **The Notifiarr application uses the API key for bi-directional authorization.**
- Must provide URL and API key for Sonarr or Radarr or Readarr or any combination.
- You may provide multiple instances using more `[[radarr]]` entries (as an example)

```none
quiet = false
debug = true
debug_log = 'C:\ProgramData\notifiarr\logs\debug.log'
[...truncated...]
log_file = 'C:\ProgramData\notifiarr\logs\log.log'
http_log = 'C:\ProgramData\notifiarr\logs\http.log'
```

### Log Files

You can set a log file in the config. You should do that. Otherwise, find your logs here:

- Linux: `/var/log/messages` or `/var/log/syslog` (w/ default syslog)
- FreeBSD: `/var/log/syslog` (w/ default syslog)
- Homebrew: `/usr/local/var/log/notifiarr.log`
- macOS: `~/.notifiarr/notifiarr.log`
- Windows: `<home folder>/.notifiarr/notifiarr.log`

#### Detailed Debugging

> Ensure that the path you set for the log files is somewhere both you and the client has access to. {.is-info}

1. Locate and Open the Notifiarr Client config file.
1. `Disable` Quiet (i.e. `quiet = false`)
1. `Enable` Debug (i.e. `debug = true`)
1. Configure a Debug Log File path

- Windows:`debug_log = 'C:\ProgramData\notifiarr\logs\debug.log'`
- Linux: `debug_log = '/etc/notifiarr/debug.log'`

1. Configure a Log Path for the Log File and HTTP Log File

- Windows Log: `log_file = 'C:\ProgramData\notifiarr\logs\log.log'`
- Windows HTTP Log: `http_log = 'C:\ProgramData\notifiarr\logs\http.log'`
- Linux Log: `log_file = '/etc/notifiarr/notifiarr.log'`
- Linux HTTP Log: `http_log = '/etc/notifiarr/http.log'`

1. Important: Make sure none of these lines start with a `#` and restart the client for the changes to take effect

#### Clearing Logs

- To `clear` logs to make troubleshooting easier - stop the client and rename/remove the log file, the restart the client.

- If you have not previously enabled debug logs you do not need to clear anything.

## ENV Variables

- No thanks

### Plex

This application can also send Plex sessions to Notifiarr so you can receive
notifications when users interact with your server. This has three different features:

- Notify all sessions on a longer interval (30+ minutes).
- Notify on session nearing completion (percent complete).
- Notify on session change (Plex Webhook) ie. pause/resume.

You must provide a [Plex Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/) for this to work. The client checks Plex once per minute looking for sessions nearing completion. If Plex goes down this will cause a lot of log spam. You will also need to add a webhook to Plex so it sends notices to the client for play/resume/database backup/etc if you want those, note the Plex Pass is required for webhooks.

- In Plex Media Server, add this URL to webhooks:
  - `http://localhost:5454/plex?token=plex-token-here`
- Replace `localhost` with the IP or host of the Notifiarr application.
- Replace `plex-token-here` with your Plex token.
- **The Notifiarr application uses the Plex token to authorize incoming webhooks.**

#### System Snapshot

This application can also take a snapshot of your system at an interval and send
you a notification. Snapshot means system health like cpu, memory, disk, raid, users, etc.

If you monitor drive health you must have smartmontools (`smartctl`) installed.
If you use smartctl on Linux, you must enable sudo. Add this sudoers entry to
`/etc/sudoers` and fix the path to `smartctl` if yours differs. If you monitor
raid and use MegaCli (LSI card), add the appropriate sudoers entry for that too.

```none
notifiarr ALL=(root) NOPASSWD:/usr/sbin/smartctl *
notifiarr ALL=(root) NOPASSWD:/usr/sbin/MegaCli64 -LDInfo -Lall -aALL
```

##### Snapshot Packages

- **Windows**:  `smartmontools` - get it here <https://sourceforge.net/projects/smartmontools/>
- **Linux**:    Debian/Ubuntu: `apt install smartmontools`, RedHat/CentOS: `yum install smartmontools`
- **Synology**: `opkg install smartmontools`, but first get Entware:
  - Entware (synology):  <https://github.com/Entware/Entware-ng/wiki/Install-on-Synology-NAS>
  - Entware Package List: <https://github.com/Entware/Entware-ng#readme>

- _Notes: Not all systems can report CPU temperatures._

#### Service Checks

The Notifiarr client can also check URLs for health. If you set names on your
Starr apps they will be automatically checked and reports sent to Notifiarr. Find the below setting and switch it to `true`

```none
[services]
  disabled = false   # Setting this to true disables all service checking routines.
```

Monitor an app:

```none
[[service]]
  name     = "App: Bazarr"
  type     = "http"
  check    = 'http://localhost:6767/system/status'
  expect   = "200"
  timeout  = "30s"
  interval = "1m0s"
```

Monitor another machine:

```none
[[service]]
  name     = "Server: webserver"
  type     = "tcp"
  check    = '10.1.0.212:80'
  expect   = "200"
  timeout  = "10s"
  interval = "1m0s"
```

Monitor a running process:

```none
[[service]]
  name     = "App: Unpackerr"
  type     = "process"
  check    = 'unpackerr.amd64.exe'
  expect   = "count:1"
  timeout  = "30s"
  interval = "1m0s"
```

## Reverse Proxy

You'll need to expose this application to the Internet, so Notifiarr.com
can make connections to it. While you can certainly poke a hole your firewall
and send the traffic directly to this app, it is recommended that you put it
behind a reverse proxy. It's pretty easy.

You'll want to tune the `upstreams` and `urlbase` settings for your environment.
If your reverse proxy IP is `192.168.3.45` then set `upstreams = ["192.168.3.45/32"]`.
The `urlbase` can be left at `/`, but change it if you serve this app from a
subfolder. We'll assume you want to serve the app from `/notifiarr/` and
it's running on `192.168.3.33` - here's a sample nginx config to do that:

```nginx
location /notifiarr/ {
  proxy_set_header X-Forwarded-For $remote_addr;
  proxy_pass http://192.168.3.33:5454$request_uri;
}
```

Make sure the `location` path matches the `urlbase` and ends with a `/`.
That's all there is to it.

Here are two more example Nginx configs:

- [TRaSH-'s Swag](https://gist.github.com/TRaSH-/037235b0440b38c8964a2cbb64179cf3) - A drop-in for Swag users.
- [Captain's Custom](https://github.com/Go-Lift-TV/organizr-nginx/blob/master/golift/notifiarr.conf) - Fits into Captain's Go Lift setup. Not for everyone.

## Docker Compose

These are just some examples from users, they may need modified to run on your system and are intended to be informational. You should decide if you are going to use ENV variables or the conf file for the settings (conf file recommended). This first example has ENV and a defined conf which means the conf settings are not used for the ENV defined ones (creates confusion which is why I added it to see and avoid doing)

- The image is the only one available. LSIO & Hotio do not provide builds.

### Example 1

```yml
notifiarr:
    container_name: notifiarr
    hostname: notifiarr
    image: golift/notifiarr:latest
    restart: unless-stopped
    privileged: true
    environment:
      - TZ=${TZ}
      - DN_SNAPSHOT_TIMEOUT=10s
      - DN_SNAPSHOT_INTERVAL=30m
      - DN_SNAPSHOT_MONITOR_DRIVES=true
      - DN_SNAPSHOT_USE_SUDO=true
      - DN_SNAPSHOT_MONITOR_CPUTEMP=true
      - DN_SNAPSHOT_MONITOR_CPUMEMORY=true
      - DN_SNAPSHOT_MONITOR_SPACE=true
      - DN_SNAPSHOT_MONITOR_RAID=true
    volumes:
      - ${BASE_DOCKER_DATA_PATH}/notifiarr/config/notifiarr.conf:/config/notifiarr.conf
      - /var/run/utmp:/var/run/utmp
    ports:
      - 5454:5454
```

### Example 2

```yml
notifiarr:
   container_name: notifiarr
   hostname: notifiarr
   image: golift/notifiarr:latest
   restart: unless-stopped
   ports:
     - 5454:5454
   environment:
     - TZ=${TZ}
   volumes:
     - ${DOCKERCONFDIR}/notifiarr:/config
     - /var/run/utmp:/var/run/utmp  # optional, only needed if you want to count users
   privileged: true    # Optional, only needed for Snapshots
```

### Example 3

```yml
notifiarr:
    image: golift/notifiarr:latest
    container_name: notifiarr
    hostname: notifiarr
    privileged: true
    volumes:
      - ${CONFDIR}/notifiarr:/config
      - ${LOGDIR}/notifiarr:/logs
      - /var/run/utmp:/var/run/utmp
    ports:
      - 5454:5454
    restart: unless-stopped
```
