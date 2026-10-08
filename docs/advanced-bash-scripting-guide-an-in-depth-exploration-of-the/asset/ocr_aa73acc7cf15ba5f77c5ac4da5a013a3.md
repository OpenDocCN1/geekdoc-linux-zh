# # Chapter 21. Subshells

Running a script launches a new process, a *subshell*.

> >**: A subshell is a child process launched by a shell (or shell script) -- the shell that gives you the prompt at the console or in an xterm window. As your commands are interpreted as the command-line prompt, similarly does a script batch-process a list of commands. Each shell script running is, in effect, a subprocess (child process) of the parent shell.

A shell script can launch itself subprocesses. These *subshells* let the script do parallel processing, in effect executing multiple tasks simultaneously.

```
##!/bin/bash
# subshell-test.sh
(
  # Inside parentheses, and therefore a subshell
  while [ 1 ] ; # Endless loop.
  do
    echo "Subshell running ."
  done
)
# Script will run forever,
# or at least until terminated by a Ctrl-C

exit $ # End of script (but will never get here)
```

Now, run the script:
sh subshell-test.sh

And, while the script is running, from a different xterm:
ps -ef | grep subshell-test.sh

| UID | PID | PPID | C | TTY | TIME | CMD |
|---|---|---|---|---|---||
| 500 | 2698 | 2502 | 0 | 14:26 pts/4 | 00:00:00 sh subshell-test.sh |
| 500 | 2699 | 2698 | 21 | 14:26 pts/4 | 00:00:24 sh subshell-test.sh |

Analysis:
PID 2698, the script, launched PID 2699, the subshell.

Note: The "UID ..." line will be filtered out by the "grep" command, but is shown here for illustrative purposes.

In general, an external command in a shell forks off a subprocess. [107] we a Bash builtin for. This reason, builtins execute more quickly and use fewer resources than their external command equivalents.

# **List Command within Parentheses**