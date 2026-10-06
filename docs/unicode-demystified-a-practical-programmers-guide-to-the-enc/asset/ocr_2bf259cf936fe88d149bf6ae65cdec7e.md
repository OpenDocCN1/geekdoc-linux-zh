# # Heading II (Continued)

The exact column title differs, depending on the type of option you use. This table shows the headings for UNIX98 (one hyphen) options.

| RSS (resident set size) | The number of blocks of memory that process is using. |
| SIZE | The size, in blocks, of the core image of the process. |
| STIME or START | The date the process started. |
| STAT or S (status) | The status of the process as specified by one or more letters from the following list: 
| < High priority |
| D Sleeping and cannot be interrupted |
| L Pages locked in memory (real-time and custom I/O) |
| N Low priority |
| R Available for execution (on run queue) |
| S Sleeping |
| T Either stopped or being traced |
| W Has no pages resident in RAM for its child processes |
| Z Zombie process that is waiting for its child processes to terminate before it terminates |
| TIME | The number of minutes and seconds that the process has been running. |
| TTY (terminal) | The name of the terminal controlling the process. |
| UID (user ID) | The user ID of the user who owns the process. |
| USER | The username of the user who owns the process. |
| WCHAN (wait channel) | If the process is waiting for an event, this column gives the address of the kernel function that caused the process to wait. It is 0 for processes that are not waiting or sleeping.

The first example shows ps, without any options, displaying the user's active processes. The first process is the shell (zsh), and the second is the process executing the ps utility:

# Examples