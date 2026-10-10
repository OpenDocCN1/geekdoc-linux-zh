# **OUTPUT FIELDS (CONT.)**

| Field | Description |
| :--- | :--- |
| SIZE | Displays the size of the code, plus data, plus stack space, in K (kilobytes). |
| RSS | Displays the total amount of physical memory in K (kilobytes). |
| SHARE | Displays the amount of shared memory in K (kilobytes). |
| STAT | Displays one of the following state codes: |
| < | Higher-priority process. |
| D | Uninterruptible sleep. |
| L | Pages locked in memory. |
| N | Lower-priority process. |
| R | Runnable. |
| S | Sleeping. |
| T | Traced or stopped. |
| W | No resident memory pages. |
| Z | Zombie process (stalled). |
| LIB | Displays the size of the library pages used in K (kilobytes). |
| %CPU | Displays the percentage of total CPU time used by this process. |
| %MEM | Displays the percentage of total physical memory used by this process. |
| TIME | Displays the total CPU time used by this process since it was started. |
| COMMAND | Displays the command name of the process. |

# **EXAMPLES**

| This Command | Does the Following |
| :--- | :--- |
| `top -1s` | Starts `top` so that zombie and idle processes are hidden, and dangerous commands are disabled. |
| M | In interactive mode, sorts by memory usage so that the biggest memory hogs are shown first. |