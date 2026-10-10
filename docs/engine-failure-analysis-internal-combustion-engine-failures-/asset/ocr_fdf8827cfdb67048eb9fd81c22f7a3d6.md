# OPTIONS (CONT.)

| Use This Option | To Do This |
|---|---|
| -T | Show all the processes on this terminal. |
| -t tty | Show processes running on the specified tty. |
| -U user ID | Show processes owned by the specified user ID (name or number). |
| -V | Display the version number. |
| -W | Use wide output. |
| -X | Show processes running without a terminal. |


# SORT KEYS

| Short Form | Long Form | Description |
|---|---|---|
| p | pid | The process ID number |
| c | cmd | The name of the executable |
| C | cmdline | The flags |
| g | pgrp | The group owner ID of the process |
| G | tgid | The group owner ID of the controlling tty process |
| j | cutime | The cumulative user time |
| J | cstime | The cumulative system time |
| k | utime | The user time |
| K | stime | The system time |
| m | min_flt | The number of minor page faults |
| M | maj_flt | The number of major page faults |
| n | cmin_flt | The cumulative minor page faults |
| N | cmaj_flt | The cumulative major page faults |
| o | session | The session ID |
| P | ppid | The process ID of the parent process |
| r | rss | The resident set size |
| R | resident | The resident pages |
| s | size | The memory usage in K (kilobytes) |