---
title: Client
description: 
published: true
date: 2022-01-09T21:12:32.768Z
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

- Linux: `/var/log/messages` or `/var/log/syslog` (w/ default syslog)
- FreeBSD: `/var/log/syslog` (w/ default syslog)
- Homebrew: `/usr/local/var/log/notifiarr.log`
- macOS: `~/.notifiarr/notifiarr.log`
- Windows: `<home folder>/.notifiarr/notifiarr.log`

### Clearing Logs

- To `clear` logs to make troubleshooting easier - simply rename the log file or delete it then restart the client.

- If you have not previously enabled debug logs you do not need to clear anything.

### Detailed Debugging

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

#### Example Config File Snippet

```none
quiet = false
debug = true
debug_log = 'C:\ProgramData\notifiarr\logs\debug.log'
[...truncated...]
log_file = 'C:\ProgramData\notifiarr\logs\log.log'
http_log = 'C:\ProgramData\notifiarr\logs\http.log'
```

> Ensure that the path you use is somewhere the client has access to. {.is-warning}

Again change the path to somewhere the client has access to.

----------

If transfers are in a Warning or Error state they will not be extracted.

Still having problems?[Let us know!](https://github.com/Notifiarr/notifiarr/issues/new) or [Come by Discord](https://discord.gg/AURf8Yz)

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
