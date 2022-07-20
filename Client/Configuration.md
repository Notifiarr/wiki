---
title: Configuration
description: 
published: true
date: 2022-07-20T00:29:38.681Z
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

> **Unraid Users**
You must configure a Notifiarr API Key in the Unraid Template. If you wish to use Plex then you'll also need to set the Plex Token and Plex URL in the template as well.
{.is-danger}

> **Docker Users**
Note that Docker Enviormental Variables - and thus the Unraid Template - override the Config file.
{.is-info}

- You can use env variables, but the conf is suggested
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

 Instead of, or in addition to a config file, you may configure a docker container with environment variables.
- Any variable not provided takes the default.
- Must provide an API key from notifiarr.com.
  - **The Notifiarr application uses the API key for bi-directional authorization.**
- You may provide multiple sonarr, radarr or readarr instances using `DN_SONARR_1_URL`, `DN_SONARR_2_URL`, etc or by duplicating the starr block in the conf file.

| Config Name   | Variable Name      | Default / Note                                                               |
| ------------- | ------------------ | ---------------------------------------------------------------------------- |
| api_key       | `DN_API_KEY`       | **Required** / API Key from Notifiarr.com                                    |
| auto_update   | `DN_AUTO_UPDATE`   | `off` / Set to `daily` to turn on automatic updates (windows only)           |
| bind_addr     | `DN_BIND_ADDR`     | `0.0.0.0:5454` / The IP and port to listen on                                |
| quiet         | `DN_QUIET`         | `false` / Turns off output. Set a log_file if this is true                   |
| ui_password   | `DN_UI_PASSWORD`   | None by default. Set a username:password & change the password to encrypt it |
| urlbase       | `DN_URLBASE`       | default: `/` Change the web root with this setting                           |
| upstreams     | `DN_UPSTREAMS_0`   | List of upstream networks that can set X-Forwarded-For                       |
| ssl_key_file  | `DN_SSL_KEY_FILE`  | Providing SSL files turns on the SSL listener                                |
| ssl_cert_file | `DN_SSL_CERT_FILE` | Providing SSL files turns on the SSL listener                                |
| log_file      | `DN_LOG_FILE`      | None by default. Optionally provide a file path to save app logs             |
| http_log      | `DN_HTTP_LOG`      | None by default. Provide a file path to save HTTP request logs               |
| log_file_mb   | `DN_LOG_FILE_MB`   | `100` / Max size of log files in megabytes                                   |
| log_files     | `DN_LOG_FILES`     | `10` / Log files to keep after rotating. `0` disables rotation               |
| file_mode     | `DN_FILE_MODE`     | `"0600"` / Unix octal filemode for new log files                             |
| timeout       | `DN_TIMEOUT`       | `60s` / Global API Timeouts (all apps default)                               |

All applications below (starr, downloaders, tautulli, plex) have a `timeout` setting.
If the configuration for an application is missing the timeout, the global timeout (above) is used.

### Secret Settings

Recommend not messing with these unless instructed to do so.

| Config Name | Variable Name     | Default / Note                                                                                    |
| ----------- | ----------------- | ------------------------------------------------------------------------------------------------- |
| extra_keys  | `DN_EXTRA_KEYS_0` | `[]` (empty list) / Add keys to allow API requests from places besides notifiarr.com              |
| mode        | `DN_MODE`         | `production` / Change application mode: `development` or `production`                             |
| debug       | `DN_DEBUG`        | `false` / Adds payloads and other stuff to the log output; very verbose/noisy                     |
| debug_log   | `DN_DEBUG_LOG`    | `""` / Set a file system path to write debug logs to a dedicated file                             |
| max_body    | `DN_MAX_BODY`     | Unlimited, `0` / Maximum debug-log body size (integer) for payloads to and from notifiarr.com     |
|             | `TMPDIR`          | `%TMP%` on Windows. Varies depending on system; must be writable if using Backup Corruption Check |

_Note: You may disable the GUI (menu item) on Windows by setting the env variable `USEGUI` to `false`._

### System Snapshot

This application can take a snapshot of your system at an interval and send
you a notification. Snapshot means system health like cpu, memory, disk, raid, users, etc.
Other data available in the snapshot: mysql health, `iotop`, `iostat` and `top` data.
Some of this may only be available on Linux, but other platforms have similar abilities.

If you monitor drive health you must have smartmontools (`smartctl`) installed.
If you use smartctl on Linux, you must enable sudo. Add the sudoers entry below to
`/etc/sudoers` and fix the path to `smartctl` if yours differs. If you monitor
raid and use MegaCli (LSI card), add the appropriate sudoers entry for that too.

To monitor application disk I/O you may install `iotop` and add the sudoers entry
for it, shown below. This feature is enabled on the website.

#### Snapshot Sudoers

The following sudoers entries are used by various snapshot features. Add them if you use the respective feature.
You can usually just put the following content into `/etc/sudoers` or `/etc/sudoers.d/00-notifiarr`.

```yml
# Allows drive health monitoring on macOS, Linux/Docker and FreeBSD.
notifiarr ALL=(root) NOPASSWD:/usr/sbin/smartctl *

# Allows disk utilization monitoring on Linux (non-Docker).
notifiarr ALL=(root) NOPASSWD:/usr/sbin/iotop *

# Allows monitoring megaraid volumes on macOS, Linux/Docker and FreeBSD.
# Rarely needed, and you'll know if you need this.
notifiarr ALL=(root) NOPASSWD:/usr/sbin/MegaCli64 -LDInfo -Lall -aALL
```

#### Snapshot Packages

- **Windows**:  `smartmontools` - get it here <https://sourceforge.net/projects/smartmontools/>
- **Linux**:
  - Debian/Ubuntu: `apt install smartmontools`
  - RedHat/CentOS: `yum install smartmontools`
- **Docker**:    It's already in the container. Lucky you! Just run the container in `--privileged` mode.
- **Synology**: `opkg install smartmontools`, but first get Entware:
  - Entware (synology):  <https://github.com/Entware/Entware-ng/wiki/Install-on-Synology-NAS>
  - Entware Package List:  <https://github.com/Entware/Entware-ng/wiki/Install-on-Synology-NAS>

#### Snapshot Configuration

There is no client configuration for snapshots (except MySQL, below).
Snapshot configuration is found on the [website](https://notifiarr.com).

#### MySQL Snapshots

You may add mysql credentials to your notifiarr configuration to snapshot mysql
service health. This feature snapshots `SHOW PROCESSLIST` and `SHOW STATUS` data.

Access to a database is not required. Example Grant:

```mysql
GRANT PROCESS ON *.* to 'notifiarr'@'localhost'
```

| Config Name         | Variable Name            | Note                                           |
| ------------------- | ------------------------ | ---------------------------------------------- |
| snapshot.mysql.name | `DN_SNAPSHOT_MYSQL_NAME` | Setting a name enables service checks of MySQL |
| snapshot.mysql.host | `DN_SNAPSHOT_MYSQL_HOST` | Something like: `localhost:3306`               |
| snapshot.mysql.user | `DN_SNAPSHOT_MYSQL_USER` | Username in the GRANT statement                |
| snapshot.mysql.pass | `DN_SNAPSHOT_MYSQL_PASS` | Password for the user in the GRANT statement   |

### Lidarr

| Config Name      | Variable Name           | Note                                                                  |
| ---------------- | ----------------------- | --------------------------------------------------------------------- |
| lidarr.name      | `DN_LIDARR_0_NAME`      | No Default. Setting a name enables service checks                     |
| lidarr.url       | `DN_LIDARR_0_URL`       | No Default. Something like: `http://lidarr:8686`                      |
| lidarr.api_key   | `DN_LIDARR_0_API_KEY`   | No Default. Provide URL and API key if you use Readarr                |
| lidarr.username  | `DN_LIDARR_0_USERNAME`  | Provide username if using backup corruption check and auth is enabled |
| lidarr.password  | `DN_LIDARR_0_PASSWORD`  | Provide password if using backup corruption check and auth is enabled |
| lidarr.http_user | `DN_LIDARR_0_HTTP_USER` | Provide username if Lidarr uses basic auth (uncommon) and BCC enabled |
| lidarr.http_pass | `DN_LIDARR_0_HTTP_PASS` | Provide password if Lidarr uses basic auth (uncommon) and BCC enabled |
| lidarr.max_body  | `DN_LIDARR_0_MAX_BODY`  | `0` (off) / How much of the response body is logged when debug is on  |

- **BCC = Backup Corruption Check**

### Prowlarr

| Config Name        | Variable Name             | Note                                                                    |
| ------------------ | ------------------------- | ----------------------------------------------------------------------- |
| prowlarr.name      | `DN_PROWLARR_0_NAME`      | No Default. Setting a name enables service checks                       |
| prowlarr.url       | `DN_PROWLARR_0_URL`       | No Default. Something like: `http://prowlarr:9696`                      |
| prowlarr.api_key   | `DN_PROWLARR_0_API_KEY`   | No Default. Provide URL and API key if you use Readarr                  |
| prowlarr.username  | `DN_PROWLARR_0_USERNAME`  | Provide username if using backup corruption check and auth is enabled   |
| prowlarr.password  | `DN_PROWLARR_0_PASSWORD`  | Provide password if using backup corruption check and auth is enabled   |
| prowlarr.http_user | `DN_PROWLARR_0_HTTP_USER` | Provide username if Prowlarr uses basic auth (uncommon) and BCC enabled |
| prowlarr.http_pass | `DN_PROWLARR_0_HTTP_PASS` | Provide password if Prowlarr uses basic auth (uncommon) and BCC enabled |
| prowlarr.max_body  | `DN_PROWLARR_0_MAX_BODY`  | `0` (off) / How much of the response body is logged when debug is on    |

### Radarr

| Config Name      | Variable Name           | Note                                                                  |
| ---------------- | ----------------------- | --------------------------------------------------------------------- |
| radarr.name      | `DN_RADARR_0_NAME`      | No Default. Setting a name enables service checks.                    |
| radarr.url       | `DN_RADARR_0_URL`       | No Default. Something like: `http://localhost:7878`                   |
| radarr.api_key   | `DN_RADARR_0_API_KEY`   | No Default. Provide URL and API key if you use Radarr                 |
| radarr.username  | `DN_RADARR_0_USERNAME`  | Provide username if using backup corruption check and auth is enabled |
| radarr.password  | `DN_RADARR_0_PASSWORD`  | Provide password if using backup corruption check and auth is enabled |
| radarr.http_user | `DN_RADARR_0_HTTP_USER` | Provide username if Radarr uses basic auth (uncommon) and BCC enabled |
| radarr.http_pass | `DN_RADARR_0_HTTP_PASS` | Provide password if Radarr uses basic auth (uncommon) and BCC enabled |
| radarr.max_body  | `DN_RADARR_0_MAX_BODY`  | `0` (off) / How much of the response body is logged when debug is on. |

### Readarr

| Config Name       | Variable Name            | Note                                                                   |
| ----------------- | ------------------------ | ---------------------------------------------------------------------- |
| readarr.name      | `DN_READARR_0_NAME`      | No Default. Setting a name enables service checks                      |
| readarr.url       | `DN_READARR_0_URL`       | No Default. Something like: `http://localhost:8787`                    |
| readarr.api_key   | `DN_READARR_0_API_KEY`   | No Default. Provide URL and API key if you use Readarr                 |
| readarr.username  | `DN_READARR_0_USERNAME`  | Provide username if using backup corruption check and auth is enabled  |
| readarr.password  | `DN_READARR_0_PASSWORD`  | Provide password if using backup corruption check and auth is enabled  |
| readarr.http_user | `DN_READARR_0_HTTP_USER` | Provide username if Readarr uses basic auth (uncommon) and BCC enabled |
| readarr.http_pass | `DN_READARR_0_HTTP_PASS` | Provide password if Readarr uses basic auth (uncommon) and BCC enabled |
| readarr.max_body  | `DN_READARR_0_MAX_BODY`  | `0` (off) / How much of the response body is logged when debug is on.  |

### Sonarr

| Config Name      | Variable Name           | Note                                                                  |
| ---------------- | ----------------------- | --------------------------------------------------------------------- |
| sonarr.name      | `DN_SONARR_0_NAME`      | No Default. Setting a name enables service checks                     |
| sonarr.url       | `DN_SONARR_0_URL`       | No Default. Something like: `http://localhost:8989`                   |
| sonarr.api_key   | `DN_SONARR_0_API_KEY`   | No Default. Provide URL and API key if you use Sonarr                 |
| sonarr.username  | `DN_SONARR_0_USERNAME`  | Provide username if using backup corruption check and auth is enabled |
| sonarr.password  | `DN_SONARR_0_PASSWORD`  | Provide password if using backup corruption check and auth is enabled |
| sonarr.http_user | `DN_SONARR_0_HTTP_USER` | Provide username if Sonarr uses basic auth (uncommon) and BCC enabled |
| sonarr.http_pass | `DN_SONARR_0_HTTP_PASS` | Provide password if Sonarr uses basic auth (uncommon) and BCC enabled |
| sonarr.max_body  | `DN_SONARR_0_MAX_BODY`  | `0` (off) / How much of the response body is logged when debug is on. |

### Downloaders

You can add supported downloaders so they show up on the dashboard integration.
You may easily add service checks to these downloaders by adding a name.
Any number of downloaders of any type may be configured.

These all also have `interval` and `timeout` represented as a Go Duration.
Examples: `1m`, `1m30s`, `3m15s`, 1h5m`. Valid units are`s`,`m`, and`h`. Combining units is additive.

#### QbitTorrent

| Config Name    | Variable Name         | Note                                                          |
| -------------- | --------------------- | ------------------------------------------------------------- |
| qbit.name      | `DN_QBIT_0_NAME`      | No Default. Setting a name enables service checks             |
| qbit.url       | `DN_QBIT_0_URL`       | No Default. Something like: `http://localhost:8080`           |
| qbit.user      | `DN_QBIT_0_USER`      | No Default. Provide URL, user and pass if you use Qbit        |
| qbit.pass      | `DN_QBIT_0_PASS`      | No Default. Provide URL, user and pass if you use Qbit        |
| qbit.http_user | `DN_QBIT_0_HTTP_USER` | Provide this username if Qbit is behind basic auth (uncommon) |
| qbit.http_pass | `DN_QBIT_0_HTTP_PASS` | Provide this password if Qbit is behind basic auth (uncommon) |

#### rTorrent

| Config Name   | Variable Name        | Note                                                       |
| ------------- | -------------------- | ---------------------------------------------------------- |
| rtorrent.name | `DN_RTORRENT_0_NAME` | No Default. Setting a name enables service checks          |
| rtorrent.url  | `DN_RTORRENT_0_URL`  | No Default. Something like: `http://localhost:5000`        |
| rtorrent.user | `DN_RTORRENT_0_USER` | No Default. Provide URL, user and pass if you use rTorrent |
| rtorrent.pass | `DN_RTORRENT_0_PASS` | No Default. Provide URL, user and pass if you use rTorrent |

#### SABnzbd

| Config Name     | Variable Name          | Note                                                        |
| --------------- | ---------------------- | ----------------------------------------------------------- |
| sabnzbd.name    | `DN_SABNZBD_0_NAME`    | No Default. Setting a name enables service checks           |
| sabnzbd.url     | `DN_SABNZBD_0_URL`     | No Default. Something like: `http://localhost:8080/sabnzbd` |
| sabnzbd.api_key | `DN_SABNZBD_0_API_KEY` | No Default. Provide URL and API key if you use SABnzbd      |

#### Deluge

| Config Name      | Variable Name           | Note                                                            |
| ---------------- | ----------------------- | --------------------------------------------------------------- |
| deluge.name      | `DN_DELUGE_0_NAME`      | No Default. Setting a name enables service checks               |
| deluge.url       | `DN_DELUGE_0_URL`       | No Default. Something like: `http://localhost:8080`             |
| deluge.password  | `DN_DELUGE_0_PASSWORD`  | No Default. Provide URL and password key if you use Deluge      |
| deluge.http_user | `DN_DELUGE_0_HTTP_USER` | Provide this username if Deluge is behind basic auth (uncommon) |
| deluge.http_pass | `DN_DELUGE_0_HTTP_PASS` | Provide this password if Deluge is behind basic auth (uncommon) |

#### NZBGet

| Config Name | Variable Name      | Note                                                            |
| ----------- | ------------------ | --------------------------------------------------------------- |
| nzbget.name | `DN_NZBGET_0_NAME` | No Default. Setting a name enables service checks               |
| nzbget.url  | `DN_NZBGET_0_URL`  | No Default. Something like: `http://localhost:6789`             |
| nzbget.user | `DN_NZBGET_0_USER` | No Default. Provide URL username and password if you use NZBGet |
| nzbget.pass | `DN_NZBGET_0_PASS` | No Default. Provide URL username and password if you use NZBGet |

### Plex

This application can also send Plex sessions to Notifiarr so you can receive notifications when users interact with your server.
This has three different features:

- Notify all sessions on a longer interval (30+ minutes).
- Notify on session nearing completion (percent complete).
- Notify on session change (Plex Webhook) ie. pause/resume.

You [must provide Plex Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/) for this to work.
You may also need to add a webhook to Plex so it sends notices to this application.

- In Plex Media Server, add this URL to webhooks:
  - `http://localhost:5454/plex?token=plex-token-here`
- Replace `localhost` with the IP or host of the notifiarr application.
- Replace `plex-token-here` with your plex token.
- **The Notifiarr application uses the Plex token to authorize incoming webhooks.**

| Config Name | Variable Name   | Note                                                                                                                                            |
| ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| plex.url    | `DN_PLEX_URL`   | `http://localhost:32400` / local URL to your plex server                                                                                        |
| plex.token  | `DN_PLEX_TOKEN` | Required. [Must provide Plex Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/) for this to work. |

### Tautulli

Only 1 Tautulli instance may be configured per client.
Providing Tautulli allows Notifiarr to use the "Friendly Name" for your Plex users and it allows you to easily enable a service check.

| Config Name      | Variable Name         | Note                                                                    |
| ---------------- | --------------------- | ----------------------------------------------------------------------- |
| tautulli.name    | `DN_TAUTULLI_NAME`    | No Default. Setting a name enables service checks of Tautulli           |
| tautulli.url     | `DN_TAUTULLI_URL`     | No Default. Something like: `http://localhost:8181`                     |
| tautulli.api_key | `DN_TAUTULLI_API_KEY` | No Default. Provide URL and API key if you want name maps from Tautulli |

### Service Checks

The Notifiarr client can also check URLs for health. If you set names on your Starr apps they will be automatically checked and reports sent to Notifiarr.
If you provide a log file for service checks, those logs will no longer write to the app log nor to console stdout.

| Config Name       | Variable Name          | Note                                                                |
| ----------------- | ---------------------- | ------------------------------------------------------------------- |
| services.log_file | `DN_SERVICES_LOG_FILE` | If a file path is provided, service check logs write there          |
| services.interval | `DN_SERVICES_INTERVAL` | `10m`, How often to send service states to Notifiarr; minimum: `5m` |
| services.parallel | `DN_SERVICES_PARALLEL` | `1`, How many services can be checked at once; 1 is plenty          |

You can also create ad-hoc service checks for things like Bazarr.

| Config Name      | Variable Name           | Note                                         |
| ---------------- | ----------------------- | -------------------------------------------- |
| service.name     | `DN_SERVICE_0_NAME`     | Services must have a unique name             |
| service.type     | `DN_SERVICE_0_TYPE`     | Type must be one of `http`, `tcp`, `process` |
| service.check    | `DN_SERVICE_0_CHECK`    | The `URL`, or `host/ip:port` to check        |
| service.expect   | `DN_SERVICE_0_EXPECT`   | `200`, For HTTP, the return code to expect   |
| service.timeout  | `DN_SERVICE_0_TIMEOUT`  | `15s`, How long to wait for service response |
| service.interval | `DN_SERVICE_0_INTERVAL` | `5m`, How often to check the service         |

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
location /notifiarr {
  proxy_set_header X-Forwarded-For $remote_addr;
  set $notifiarr http://192.168.3.33:5454;
  proxy_pass $notifiarr$request_uri;
}
```

Make sure the Nginx `location` path matches the `urlbase` Notifiarr setting.
That's all there is to it.

Using an auth proxy? Be sure to set `ui_password` to the string `"webauth"`.
The Nginx config looks more like this:

```nginx
location /notifiarr/api {
  proxy_set_header X-Forwarded-For $remote_addr;
  set $notifiarr http://192.168.3.33:5454;
  proxy_pass $notifiarr$request_uri;
}

location /notifiarr {
  proxy_set_header X-Forwarded-For $remote_addr;
  proxy_set_header X-WebAuth-User $_username;
  set $notifiarr http://192.168.3.33:5454;
  proxy_pass $notifiarr$request_uri;
}
```

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
