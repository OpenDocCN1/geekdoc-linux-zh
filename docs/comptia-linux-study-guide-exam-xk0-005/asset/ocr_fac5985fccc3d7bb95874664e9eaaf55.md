| Command | Description |
| :--- | :--- |
| < or > | Moves the sort field one column left (<) or right (>) |
| r | Toggles normal or reverse sort order |
| h | Toggles showing of threads |
| c | Toggles showing of the command name or the full command line (including parameters) of processes |
| i | Toggles showing of idle processes |
| S | Toggles showing of the cumulative CPU time or relative CPU time |
| x | Toggles highlighting of the sort field |
| y | Toggles highlighting of running tasks |
| z | Toggles color and mono mode |
| u | Shows processes for a specific user |
| n or # | Sets the number of processes to display |
| k | Kills a specific process (only if process owner or if root user) |
| r | Changes the priority (renice) of a specific process (only if process owner or if root user) |
| d or s | Changes the update interval (default 3 seconds) |
| W | Writes current settings to a configuration file |
| q | Exits the top command |

You have lots of control over the output of the top command. Use the F or O command to toggle which field the sort order is based on. You can also use the r interactive command to reverse the current sorting. Using this tool, you can often find offending processes that have taken over your system. A relatively new utility, the htop program is an improved version of the top utility, available in most Linux distributions as an additional software package that you can install. Figure 21.2 shows an example of the htop output display.