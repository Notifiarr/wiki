---
title: Client
description: 
published: true
date: 2021-08-16T01:01:08.967Z
tags: 
editor: markdown
dateCreated: 2021-05-22T01:08:20.353Z
---

<img src="https://docs.notifiarr.com/img/repo-logo.png">

This is the unified client for [Notifiarr.com](https://notifiarr.com).
The client enables content requests from Media Bot in your Discord Server.
It also provides reports for Plex usage and system health.

## Troubleshooting

- Find help on [GoLift Discord](https://golift.io/discord).
- And/or on [Notifiarr Discord](https://discord.gg/AURf8Yz).

Log files:

You can set a log file in the config. You should do that. Otherwise, find your logs here:

-   Linux: `/var/log/messages` or `/var/log/syslog` (w/ default syslog)
-   FreeBSD: `/var/log/syslog` (w/ default syslog)
-   Homebrew: `/usr/local/var/log/notifiarr.log`
-   macOS: `~/.notifiarr/notifiarr.log`
-   Windows: `<home folder>/.notifiarr/notifiarr.log`


### Detailed Debugging

In the conf file, find `quiet = true` or it may be false, change it to
```
quiet = false
debug = true
debug_log = 'C:\ProgramData\notifiarr\logs\debug.log'
```

Change this path to somewhere the client has access to.

Next find the `log_file =` line and change it to
```
log_file = 'C:\ProgramData\notifiarr\logs\log.log'
http_log = 'C:\ProgramData\notifiarr\logs\http.log'
```

Again change the path to somewhere the client has access to.

- Important: Make sure none of these lines start with a `#` and restart the client after these changes

----------

If transfers are in a Warning or Error state they will not be extracted.

Still having problems?
[Let us know!](https://github.com/Notifiarr/notifiarr/issues/new)

## Integrations

The following fine folks are providing their services, completely free! These service
integrations are used for things like storage, building, compiling, distribution and
documentation support. This project succeeds because of them. Thank you!

<p style="text-align: center;">
<a title="PackageCloud" alt="PackageCloud" href="https://packagecloud.io"><img src="https://docs.golift.io/integrations/packagecloud.png"/></a>
<a title="GitHub" alt="GitHub" href="https://GitHub.com"><img src="https://docs.golift.io/integrations/octocat.png"/></a>
<a title="Docker Cloud" alt="Docker" href="https://cloud.docker.com"><img src="https://docs.golift.io/integrations/docker.png"/></a>
<a title="Travis-CI" alt="Travis-CI" href="https://Travis-CI.com"><img src="https://docs.golift.io/integrations/travis-ci.png"/></a>
<a title="Homebrew" alt="Homebrew" href="https://brew.sh"><img src="https://docs.golift.io/integrations/homebrew.png"/></a>
<a title="Go Lift" alt="Go Lift" href="https://golift.io"><img src="https://docs.golift.io/integrations/golift.png"/></a>
</p>

## Contributing

Yes, please.

## License

[MIT](https://github.com/Notifiarr/notifiarr/blob/main/LICENSE) - Copyright (c) 2020-2021 Go Lift