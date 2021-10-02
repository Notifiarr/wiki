---
title: Installation
description: 
published: true
date: 2021-10-02T12:29:06.130Z
tags: 
editor: markdown
dateCreated: 2021-05-22T01:08:57.387Z
---

## Installation

### Linux

Linux repository hosting provided by
[![packagecloud](https://docs.golift.io/integrations/packagecloud-full.png "PackageCloud.io")](http://packagecloud.io)

This works on any system with apt or yum. If your system does not use APT or YUM, then download a package from the [Releases](https://github.com/Notifiarr/notifiarr/releases) page.
Install the Go Lift package repo and Notifiarr with this command:
```
curl -s https://golift.io/repo.sh | sudo bash -s - notifiarr
```

After install, edit the config and start the service:

```
sudo nano /etc/notifiarr/notifiarr.conf
sudo service systemctl restart notifiarr -or- sudo service notifiarr restart
```

### FreeBSD

-   Download a package from the [Releases](https://github.com/Notifiarr/notifiarr/releases) page.
-   Install it, edit config, start it.

Example of the above in shell form:

```shell
wget -qO- https://raw.githubusercontent.com/Notifiarr/notifiarr/main/scripts/install.sh | sudo bash

vi /usr/local/etc/notifiarr/notifiarr.conf
service notifiarr start
```

On Linux and FreeBSD, Notifiarr runs as `user:group` `notifiarr:notifiarr`.

### macOS Install

#### Homebrew

-   Edit config file at `/usr/local/etc/notifiarr/notifiarr.conf`
-   Start it.
-   Like this:

```shell
brew install golift/mugs/notifiarr
vi /usr/local/etc/notifiarr/notifiarr.conf
brew services start notifiarr
```

#### macOS App

-   You can use the unsigned app on the Releases page.
-   You must right click the app and select `Open` so macOS allows it.
-   When you open it for the first time it will create a config file and log file:
    -   `~/.notifiarr/notifiarr.conf`
    -   `~/.notifiarr/notifiarr.log`
-   Edit the config file and reload or restart the app.

### Windows

-   Extract a `.exe.zip` file from [the Releases page](https://github.com/Notifiarr/notifiarr/releases).
-   Run the `notifiarr.amd64.exe` binary. This starts the app in the system tray.
-   When you open it for the first time it will create a config file and log file:
    -   `C:\ProgramData\notifiarr\notifiarr.conf`
    -   `<your home folder>\.notifiarr\notifiarr.log`
-   Edit the new config file suit your environment then reload or restart the app.

### Docker

This project builds automatically in [Docker Cloud](https://hub.docker.com/r/golift/notifiarr)
and creates [ready-to-use multi-architecture images](https://hub.docker.com/r/golift/notifiarr/tags).
The `latest` tag is always a tagged release in GitHub. The `main` tag corresponds
to the `main` branch in GitHub and may be broken.

#### Docker Config File

-   Copy the [example config file](https://github.com/Notifiarr/notifiarr/blob/main/examples/notifiarr.conf.example) from this repo.
-   Then grab the image from docker hub and run it using an overlay for the config file.
-   You must set `privileged` to use `smartctl` (`monitor_drives`) and/or `MegaCli` (`monitor_raid`).
-   Map the `/var/run/utmp` volume if you want to count users.
-   Mount any volumes you want to report storage space for. Where does not matter, "where" is the "name".

```shell
docker pull golift/notifiarr
docker run -d \
-v /your/config/notifiarr.conf:/config/notifiarr.conf \
-v /var/run/utmp:/var/run/utmp \
golift/notifiarr
docker logs <container id from docker run>
```

> If you're behind a reverse proxy and facing connection issues (for example after a certificate renewal), the upstreams setting in the config file might need to be changed to 
`upstreams = [ "notifiarr/32", "::1/128" ]`
{.is-info}


#### Docker Environment Variables

See below for more information about which environment variables are available.
You must set `--privileged` when `monitor_drives=true`.

```shell
docker pull golift/notifiarr
docker run -d --privileged \
  -v /var/run/utmp:/var/run/utmp \
  -e "DN_API_KEY=abcdef-12345-bcfead-43312-bbbaaa-123" \
  -e "DN_SONARR_0_URL=http://localhost:8989" \
  -e "DN_SONARR_0_API_KEY=kjsdkasjdaksdj" \
  -e "DN_SNAPSHOT_MONITOR_DRIVES=true" \
  golift/notifiarr
docker logs <container id from docker run>
```
