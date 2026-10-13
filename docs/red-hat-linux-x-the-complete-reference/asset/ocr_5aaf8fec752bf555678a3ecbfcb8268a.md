# Tip

You can also shut down your system from the GNOME or KDE desktop.

The shutdown options are listed in Table 27-4.

Table 27-4: System Shutdown Options

| Command | Description |
|---|---|
| `shutdown [-rkh ncft]`
`time [warning-message]` | Shuts the system down after the specified time period, issuing warnings to users; you can specify a warning message of your own after the time argument; if neither -h nor -r is specified to shut down the system, the system sets to the administrative mode, runlevel state 1. |
| **Argument** | |
| **Time** | Has two possible formats: it can be an absolute time in the format `hh:mm`, with `hh` as the hour (one or two digits) and `mm` as the minute (in two digits); it can also be in the format `+m`, with `m` as the number of minutes to wait; the word `now` is an alias for `+0`. |
| **Option** | |
| `-t sec` | Tells `init` to wait `sec` seconds between sending processes the warning and the kill signals, before changing to another runlevel. |
| `-k` | Doesn't actually shut down; only sends the warning messages to everybody. |
| `-r` | Reboots after shutdown, runlevel state 6. |
| `-h` | Halts after shutdown, runlevel state 0. |
| `-n` | Doesn't call `init` to do the shutdown; you do it yourself. |