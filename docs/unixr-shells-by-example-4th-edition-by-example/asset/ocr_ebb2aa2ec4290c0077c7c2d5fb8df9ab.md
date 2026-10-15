# 8.10.2 Shell Built-In Commands

The shell has a number of commands that are built into its source code. Because the commands are built-in, the shell doesn't have to locate them on disk, making execution much faster. The built-in commands are listed in Table 8.9.

# Table 8.9 Built-In Commands

| Command | What It Does |
|---|---|
| : | Do-nothing command; returns exit status 0 |
| . file | The dot command reads and executes command from file |
| break [n] | See "The break Command" on page 361 |
| cd | Change directory |
| continue [n] | See "The continue Command" on page 362 |
| echo [ args ] | Echo arguments |
| eval command | Shell scans the command line twice before execution |
| exec command | Runs command in place of this shell |
| exit [ n ] | Exit the shell with status n |
| export [ var ] | Make var known to subshells |
| hash | Controls the internal hash table for quicker searches for commands |
| kill [ -signal ] process | Sends the signal to the PID number or job number of the process; see /usr/include/sys/signal.h for a list of signals |
| getopts | Used in shell scripts to parse command line and check for legal options |
| login [ username ] | Sign onto the system |
| newgrp [ arg ] | Logs a user into a new group by changing the real group and effective group ID |
| pwd | Print present working directory |
| read [ var ] | Read line from standard input into variable var |
| readonly [ var ] | Make variable var read-only; cannot be reset |
| return [ n ] | Return from a function where n is the exit value given to the return |
| set | See Table 8.8 |
| shift [ n ] | Shift positional parameters to the left n times |