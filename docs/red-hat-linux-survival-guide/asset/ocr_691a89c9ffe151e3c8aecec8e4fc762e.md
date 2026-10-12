top also allows you to perform interactive tasks on processes. For example, if you press the H key while top is running you will see the following output screen:

```
Proc-Top Revision 1.2
Secure mode off; cumulative mode off; noidle mode off
```

Interactive commands are:

| Key | Description |
|---|---|
| space | Update display |
| ^L | Redraw the screen |
| fF | add and remove fields |
| oO | Change order of displayed fields |
| h or ? | Print this list |
| S | Toggle cumulative mode |
| i | Toggle display of idle processes |
| I | Toggle between Irix and Solaris views (SMP-only) |
| c | Toggle display of command name/line |
| l | Toggle display of load average |
| m | Toggle display of memory information |
| t | Toggle display of summary information |
| k | Kill a task (with any signal) |
| r | Renice a task |
| N | Sort by PID (Numerically) |
| A | Sort by age |
| P | Sort by CPU usage |
| M | Sort by resident memory usage |
| T | Sort by time / cumulative time |
| u | Show only a specific user |
| n or # | Set the number of process to show |
| s | Set the delay in seconds between updates |
| W | Write configuration file ~/.toprc |
| q | Quit |

Press any key to continue