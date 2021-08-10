---
title: Configuration
description: 
published: true
date: 2021-05-26T02:57:00.350Z
tags: 
editor: markdown
dateCreated: 2021-05-22T01:09:34.150Z
---

## Configuration Information

-   Instead of, or in addition to a config file, you may configure a docker
    container with environment variables.
-   Any variable not provided takes the default.
-   Must provide an API key from notifiarr.com.
    -   **The Notifiarr application uses the API key for bi-directional authorization.**
-   Must provide URL and API key for Sonarr or Radarr or Readarr or any combination.
-   You may provide multiple sonarr, radarr or readarr instances using
    `DN_SONARR_1_URL`, `DN_SONARR_2_URL`, etc.

|Config Name|Variable Name|Default / Note|
|---|---|---|
api_key|`DN_API_KEY`|**Required** / API Key from Notifiarr.com|
bind_addr|`DN_BIND_ADDR`|`0.0.0.0:5454` / The IP and port to listen on|
quiet|`DN_QUIET`|`false` / Turns off output. Set a log_file if this is true|
urlbase|`DN_URLBASE`|default: `/` Change the web root with this setting|
upstreams|`DN_UPSTREAMS_0`|List of upstream networks that can set X-Forwarded-For|
ssl_key_file|`DN_SSL_KEY_FILE`|Providing SSL files turns on the SSL listener|
ssl_cert_file|`DN_SSL_CERT_FILE`|Providing SSL files turns on the SSL listener|
log_file|`DN_LOG_FILE`|None by default. Optionally provide a file path to save app logs|
http_log|`DN_HTTP_LOG`|None by default. Provide a file path to save HTTP request logs|
log_file_mb|`DN_LOG_FILE_MB`|`100` / Max size of log files in megabytes|
log_files|`DN_LOG_FILES`|`10` / Log files to keep after rotating. `0` disables rotation|
timeout|`DN_TIMEOUT`|`60s` / Global API Timeouts (all apps default)|

#### Sonarr

|Config Name|Variable Name|Note|
|---|---|---|
sonarr.name|`DN_SONARR_0_NAME`|No Default. Setting a name enabled service checks.|
sonarr.url|`DN_SONARR_0_URL`|No Default. Something like: `http://localhost:8989`|
sonarr.api_key|`DN_SONARR_0_API_KEY`|No Default. Provide URL and API key if you use Sonarr|

#### Radarr

|Config Name|Variable Name|Note|
|---|---|---|
radarr.name|`DN_RADARR_0_NAME`|No Default. Setting a name enabled service checks.|
radarr.url|`DN_RADARR_0_URL`|No Default. Something like: `http://localhost:7878`|
radarr.api_key|`DN_RADARR_0_API_KEY`|No Default. Provide URL and API key if you use Radarr|

#### Readarr

|Config Name|Variable Name|Note|
|---|---|---|
readarr.name|`DN_READARR_0_NAME`|No Default. Setting a name enabled service checks.|
readarr.url|`DN_READARR_0_URL`|No Default. Something like: `http://localhost:8787`|
readarr.api_key|`DN_READARR_0_API_KEY`|No Default. Provide URL and API key if you use Readarr|

#### Lidarr

|Config Name|Variable Name|Note|
|---|---|---|
lidarr.name|`DN_LIDARR_0_NAME`|No Default. Setting a name enabled service checks.|
lidarr.url|`DN_LIDARR_0_URL`|No Default. Something like: `http://lidarr:8686`|
lidarr.api_key|`DN_LIDARR_0_API_KEY`|No Default. Provide URL and API key if you use Readarr|

#### Plex

This application can also send Plex sessions to Notfiarr so you can receive
notifications when users interact with your server. This has three different features:

- Notify all sessions on a longer interval (30+ minutes).
- Notify on session nearing completion (percent complete).
- Notify on session change (Plex Webhook) ie. pause/resume.

You [must provide Plex Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)
for this to work. Setting `movies_percent_complete` or `series_percent_complete` to a number above 0 will cause this
application to poll Plex once per minute looking for sessions nearing completion. If Plex goes down
this will cause a lot of log spam. You may also need to add a webhook to Plex so it sends notices to this application.

- In Plex Media Server, add this URL to webhooks:
  - `http://localhost:5454/plex?token=plex-token-here`
- Replace `localhost` with the IP or host of the notifiarr application.
- Replace `plex-token-here` with your plex token.
- **The Notifiarr application uses the Plex token to authorize incoming webhooks.**

|Config Name|Variable Name|Note|
|---|---|---|
plex.url|`DN_PLEX_URL`|`http://localhost:32400` / local URL to your plex server|
plex.token|`DN_PLEX_TOKEN`|Required. [Must provide Plex Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/) for this to work.|
plex.interval|`DN_PLEX_INTERVAL`|`30m`, How often to notify on all session data (cron)|
plex.cooldown|`DN_PLEX_COOLDOWN`|`10s`, Maximum rate of notifications is 1 every cooldown interval|
plex.account_map|`DN_PLEX_ACCOUNT_MAP`|map an email to a name, ex: `"som@ema.il,Name|some@ther.mail,name"`|
plex.server|`DN_PLEX_SERVER`|Optional name of this server; discovered automatically otherwise|
plex.movies_percent_complete|`DN_PLEX_MOVIES_PERCENT_COMPLETE`|Send complete notice when a movie reaches this percent.|
plex.series_percent_complete|`DN_PLEX_SERIES_PERCENT_COMPLETE`|Send complete notice when a show reaches this percent.|

#### System Snapshot

This application can also take a snapshot of your system at an interval and send
you a notification. Snapshot means system health like cpu, memory, disk, raid, users, etc.

If you monitor drive health you must have smartmontools (`smartctl`) installed.
If you use smartctl on Linux, you must enable sudo. Add this sudoers entry to
`/etc/sudoers` and fix the path to `smartctl` if yours differs. If you monitor
raid and use MegaCli (LSI card), add the appropriate sudoers entry for that too.

```
notifiarr ALL=(root) NOPASSWD:/usr/sbin/smartctl *
notifiarr ALL=(root) NOPASSWD:/usr/sbin/MegaCli64 -LDInfo -Lall -aALL
```

###### Snapshot Packages

  - **Windows**:  `smartmontools` - get it here https://sourceforge.net/projects/smartmontools/
  - **Linux**:    Debian/Ubuntu: `apt install smartmontools`, RedHat/CentOS: `yum install smartmontools`
  - **Synology**: `opkg install smartmontools`, but first get Entware:
    - Entware (synology):  https://github.com/Entware/Entware-ng/wiki/Install-on-Synology-NAS
    - Entware Package List: https://github.com/Entware/Entware-ng#readme

###### Snapshot Configuration

|Config Name|Variable Name|Note|
|---|---|---|
snapshot.interval|`DN_SNAPSHOT_INTERVAL`|`30m`, How often to send a snapshot (cron)|
snapshot.timeout|`DN_SNAPSHOT_TIMEOUT`|`10s`, How long to wait for a reply from Notifiarr.com|
snapshot.monitor_raid|`DN_SNAPSHOT_MONITOR_RAID`|Set `true` to report `mdadm` and `megacli`|
snapshot.monitor_drives|`DN_SNAPSHOT_MONITOR_DRIVES`|Set `true` to report SMART on drives|
snapshot.monitor_space|`DN_SNAPSHOT_MONITOR_SPACE`|Set `true` to report drive volume usage|
snapshot.monitor_uptime|`DN_SNAPSHOT_MONITOR_UPTIME`|Set `true` to report Local Host Information|
snapshot.monitor_cpuMemory|`DN_SNAPSHOT_MONITOR_CPUMEMORY`|Set `true` to report CPU and Memory usage|
snapshot.monitor_cpuTemp|`DN_SNAPSHOT_MONITOR_CPUTEMP`|Set `true` to report CPU temperatures|
snapshot.zfs_pools|`DN_SNAPSHOT_ZFS_POOL_0`|Provide a list of zfs pools to monitor, ie. `data`|
snapshot.use_sudo|`DN_SNAPSHOT_USE_SUDO`|Set `true` if `monitor_drives=true` or you use `megacli` on Linux|

- _Notes: Not all systems can report CPU temperatures._

#### Service Checks

The Notifiarr client can also check URLs for health. If you set names on your
Starr apps they will be automatically checked and reports sent to Notifiarr.

|Config Name|Variable Name|Note|
|---|---|---|
services.interval|`DN_SERVICES_INTERVAL`|`10m`, How often to check service health; minimum: `5m`|
services.parallel|`DN_SERVICES_PARALLE`|`1`, How many services can be checked at once; 1 is plenty|

You can also create ad-hoc service checks for things like Bazarr.

|Config Name|Variable Name|Note|
|---|---|---|
service.name|`DN_SERVICE_0_NAME`|Services must have a unique name|
service.type|`DN_SERVICE_0_TYPE`|Type must be one of `http`, `tcp`|
service.check|`DN_SERVICE_0_CHECK`|The `URL`, or `host/ip:port` to check|
service.expect|`DN_SERVICE_0_EXPECT`|`200`, For HTTP, the return code to expect|
service.timeout|`DN_SERVICE_0_TIMEOUT`|`15s`, How long to wait for service response|

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

```
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