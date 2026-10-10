# top

**top [option]**  
Launches an interactive program that enables you to track running processes. See the *Interactive Commands* table for the commands you can use once *top* is running. This utility highlights the processes that are consuming the greatest amount of CPU time and provides a wealth of additional information. See the *Output Fields* table in this section for an explanation of the *top* command's column headers.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-c` | Display entire command line not just the command name |
| `-d n` | Specify the delay between refreshes in *n* seconds |
| `-l` | Do not show idle or zombie processes |
| `-q` | Refresh without any delay |
| `-s` | Disable dangerous commands |
| `-S` | Display cumulative CPU times |
| `-n n` | Refresh the display *n* times and then exit |

# INTERACTIVE COMMANDS

| Use This Command | To Do This |
| :--- | :--- |
| `c` | Toggle the display of the command name or the full command line. |
| `Ctrl + l` | Redraw the screen. |
| `h, ?` | Show available commands. |
| `k` | Kill a process. You will be prompted for the process ID. |
| `l` | Toggle display of idle and zombie processes. |
| `n, #` | Specify the number of processes to show. You will be prompted for the number. By default, **top** shows as many processes as will fit on the display. |