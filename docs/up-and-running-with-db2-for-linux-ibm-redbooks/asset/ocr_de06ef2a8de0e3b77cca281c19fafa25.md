If you are not using batch mode to run Top, then when the output screen of Top displays, you can use the interactive command to control the display. For example, you can toggle off/on the display of CPU states, or sort the processes list by the memory occupancy percentage, or kill a process in the list. Table 6-2 shows some commonly used commands.

# Table 6-2 Frequently used interactive commands for Top

| Commands | Description |
|---|---|
| space | Immediately updates the display. |
| h or ? | Displays a help screen giving a brief summary of commands, and the status of secure and cumulative modes. |
| n or # | Changes the number of processes to display. You will be prompted to enter the number. |
| q | Quit. |
| f or F | Adds fields to display or remove fields from the display. |
| c | Toggles display of command name or full command line. |
| A | Sorts tasks by age (newest first). |
| P | Sorts tasks by CPU usage (default). |
| M | Sorts tasks by memory usage. |
| W | Writes current setup to top configuration file ~/.toprc. |

Example 6-8 shows using Top, where some interactive commands are used, such as press "M" to re-order the processes list by resident memory usage (by default, it is ordered by process ID), press "c" to toggle full command line display, and using "n" to control the number of tasks that will be displayed.

# Example 6-8 Using Top to monitor system resource usage

```
2:21pm up 2:18, 3 users, load average: 1.75, 1.77, 1.37
74 processes: 71 sleeping, 3 running, 0 zombie, 0 stopped
CPU states: 1.1% user, 0.9% system, 0.0% nice, 97.8% idle
Mem: 578608K av, 448292K used, 130316K free, 0K shrd, 78904K buff
Swap: 1753304K av, 0K used, 1753304K free 290556K cached

PID USER PRI NI SIZE RSS SHARE STAT %CPU %MEM TIME COMMAND
820 root 5 -10 23288 18M 5284 S < 0.1 3.2 16:34 X
1538 root 15 0 14136 13M 9328 S 0.0 2.4 0:12 nautilus
1545 root 15 0 12608 12M 8604 S 0.1 2.1 4:36 rhp-applet-gui
1536 root 15 0 10676 10M 8172 R 0.3 1.8 17:36 gnome-panel
1556 root 15 0 8648 8644 6752 S 0.0 1.4 0:08 gnome-terminal
1551 root 15 0 8468 8464 6828 S 0.0 1.4 0:02 gweather-applet
```