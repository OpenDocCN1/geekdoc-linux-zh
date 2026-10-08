# who — Report Who is on the System

# Synopsis

+   - /usr/bin/who [-abdHlmpqqrstTu] [file]
- /usr/bin/who -q [-n x] [file]
- /usr/bin/who am i
- /usr/bin/who am I
- /usr/xpg4/bin/who [-abdHlmpqqrtTu] [file]
- /usr/xpg4/bin/who -q [-n x] [file]
- /usr/xpg4/bin/who -s [-bdHlmpqrtu] [file]
- /usr/xpg4/bin/who am i
- /usr/xpg4/bin/who am I

# Description

The who command displays information about the current status of the system. It can list the user's name, terminal line, login time, elapsed time since activity occurred along the line, and the process ID of the command interpreter (shell) for each current UNIX user. It examines the /var/adm/utmpx file to obtain its information. If you specify file that (which must be in utmpx(4) format) is examined. Usually, file is /var/adm/utmpx, which contains a history of all logins since the file was created.
The general format for output is as follows:

```
name [state] line time [idle] [pid] [comment] [exit]
```

where:

| name | User's login name |
| state | Capability of writing to the terminal. |
| line | Name of the line found in /dev. |
| time | Time since user's login. |
| idle | Time elapsed since the user's last activity. |
| pid | User's process ID. |
| comment | Comment line in initab(4). |
| exit | Exit status for dead processes. |

> Note — After a shutdown to the single-user state, which returns a prompt. Because /var/adm/utmpx is updated at login time and there is no login in single-user state, who cannot report accurately on this state. who am i, however, returns the correct information.

# Options

+   -a Process /var/adm/utmp or the named file with -b, -d, -l, -p, -r, -t, -T, and -u options turned on.
-b Indicate the time and date of the last reboot.