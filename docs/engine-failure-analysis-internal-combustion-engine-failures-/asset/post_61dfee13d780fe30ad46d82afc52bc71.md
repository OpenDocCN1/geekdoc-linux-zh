
# OPTION

| **Use This Option** | **To Do This** |
| :--- | :--- |
| -r | Remove the hashed command |

# EXAMPLES

| **This Command** | **Does the Following** |
| :--- | :--- |
| hash tmkfdir cdrecord blaedenc | Creates hash entries for the specified commands. |
| hash | Displays the current list of hashed commands. |

# history

history [ option ] [ lines ]

Displays a numbered list of the commands you have used in this and previous sessions. You can specify the maximum number of lines to display. If the history list contains more lines than you specified, you see the most recently used commands.

# OPTIONS

| **Use This Option** | **To Do This** |
| :--- | :--- |
| -a | Write current session's commands to .bash_history |
| -n | Add to .bash_history any commands that are not yet listed in the history list |
| -r | Use .bash_history as the history list, discarding commands used in the current session |
| -w | Overwrite .bash_history with the commands used in this session |

# EXAMPLES

| **This Command** | **Does the Following** |
| :--- | :--- |
| history \| less | Displays the current history list and pipe to less for convenient reading. |
| history -n | Adds this session's new commands to .bash_history. |

# jobs

```
jobs [ option ] [ job ID ]
```

Lists all running or suspended jobs.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -l | List job IDs and process IDs |
| -n | List only those jobs that have been altered since the last time this command was used |
| -p | List process IDs only |
| -x command | Replace the command being used with the specified command |

# kill

```
kill [ option ] id
```

Terminate the process specified by id. To kill the process, you must be the owner or have superuser status (see su in Chapter 1). For a list of signals and signal IDs, see the “Signals” section in this chapter.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -signal n | Use the signal specified by n. To see a list with numbers, use kill -I. |
| -I | List the available signal names and numbers. |
| -s signal | Specify the signal by name. |

# EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| kill 5047 | Kills the specified process. |

# killall

killall [ option ] [ name ]

This utility kills processes by name or filename rather than by ID number (see kill). In the command, name can refer to a command or, if preceded by a slash mark, to a file. In either case, this command kills all processes that use the specified name or file.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -signal | Send the specified signal to the process. For a list, see the "Signals" section in this chapter. |
| -e | Require an exact match for long names (those longer than 15 characters). By default, killall will kill every process that has a name matching within 15 characters. |
| -i | Ask for confirmation before killing processes. |
| -I | List signal names and ID numbers. |
| -q | Hide program messages. |
| -v | Show all program messages. |
| -w | Wait for killed processes to die before exiting. |

# nice

nice [ option ] [ command [ argument] ]

Displays or adjusts the scheduling priority of a job. When used without specifying a command, nice displays the current scheduling priority. The range extends from the highest priority (−20) to the lowest (19). If you specify a command with the −ADJUST option, nice executes the command with a priority of 10. You will need super-user privileges to use negative priorities.

See also renice.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| −ADJUST | Execute the specified command with a priority of 10 |
| −n | Execute the specified command with a priority of n |

# nohup

```
nohup command
```

This utility executes the specified command so that it ignores SIGHUP (hang up) signals. The command can continue executing in the background even after you log out of your current user session.

# printenv

```
printenv [ variable]
```

When used without specifying a variable, this utility displays the values of all variables in the current environment. To view this utility's value, specify a variable.

# ps

```
`ps` [ `option` ] [ `sort key` ] [ `output field` ]
```

Displays a list of running processes. To make the command output easier to read, you can specify one of the sort keys listed in the Sort Keys table. You can also use one of the output fields listed in the Output Fields table.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -a | Show all processes on the current terminal, including those of other users. |
| -A | Show all processes (same as -e). |
| -C name | Show process specified by name. |
| -d | Show all but omit session leaders. |
| -e | Show all processes (same as -A). |
| -f | Use the full listing. |
| -G group ID | Show processes owned by the specified group ID (name or number). |
| -g name | Show processes owned by the session leader or group name specified by name. |
| -H | Show the process hierarchy. |
| -help | Show the available commands. |
| -j | Use the jobs format. |
| -l | Use the long format. |
| -p process ID | Show the process specified by process ID. |
| -r | Restrict the output to running processes. |
| -sort -key | Sort the output using the specified sort key (see the Sort Keys table). Use the long form of the sort key. Specify a minus sign before the key to reverse the default sort order. |
| -s session ID | Show the processes specified by session ID. |
| -T | Show all the processes on this terminal. |
| -t tty | Show processes running on the specified tty. |
| -U user ID | Show processes owned by the specified user ID (name or number). |
| -V | Display the version number. |
| -W | Use wide output. |
| -X | Show processes running without a terminal. |

# SORT KEYS

| Short Form | Long Form | Description |
| :--- | :--- | :--- |
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
| S | share | The number of shared memory pages |
| t | tty | The ID number of the tty device |
| T | start_time | The time the process was started |
| U | uid | The ID number of the process owner |
| u | user | The username of the process owner |
| v | vszie | The virtual memory usage in K (kilobytes) |
| y | priority | The kernel scheduling priority |

# OUTPUT FIELDS

| Field | Description |
| :--- | :--- |
| F | Displays one of the following process flags: |
| | **001** | Alignment warning. |
| | **002** | Being created. |
| | **004** | Shutting down. |
| | **010** | Being traced. |
| | **020** | Tracing system calls. |
| | **040** | Forked but did not exec. |
| | **100** | Run by superuser. |
| | **200** | Dropped core. |
| | **400** | Killed. |
| S, STAT | Displays the state codes: |
| | **<** | Higher-priority process. |
| | **D** | Uninterruptible sleep. |
| | **L** | Pages locked in memory. |
| | **N** | Lower-priority process. |
| | **R** | Runnable. |
| | **S** | Sleeping. |
| | **T** | Traced or stopped. |
| | **W** | No resident memory pages. |
| | **Z** | Zombie process (stalled). |
| UID | Displays the user ID. |
| PPID | Displays the parent process ID. |
| PRI | Displays the process scheduling priority. |
| NI | Displays the `nice` value. |
| SZ | Displays the amount of physical memory used. |
| VSZ | Displays the amount of virtual memory used. |
| RSS | Displays the size of resident set memory. |
| WCHAN | Displays the related kernel function. |
| TTY | Displays the name of the terminal in use for this process. |
| TIME | Displays the cumulative time of execution. |
| CMD | Displays the name of the executable. |

# EXAMPLES

| **This Command** | **Does the Following** |
| :--- | :--- |
| `ps` | Displays a list of every running process on the current terminal. |
| `ps -e` | Displays a list of all running processes. |
| `ps -eH` | Displays a list of all running processes and shows the relationship between parent and child processes. |
| `ps -el - -sort -size` | Displays a verbose list of all running processes, sorted by the amount of memory used. The biggest memory hogs are listed first. |

# readonly

```
readonly [ `variable` ]
```

Makes the specified `variable` read-only so that its value cannot be changed. When used without a `variable` name, displays all current read-only variables.
