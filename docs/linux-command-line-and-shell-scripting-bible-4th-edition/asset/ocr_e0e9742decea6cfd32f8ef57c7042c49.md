| -r | Starts a restricted shell, limiting the user to the default directory |
| -s | Reads commands from the standard input |

You can find more help on the `bash` command and even more command-line parameters by typing **man bash** . The `bash --help` command provides additional assistance as well.

> TIP
> 
> **If you'd like to see the version of the Bash shell, just type `bash --version` at the command line. This won't create a subshell, but instead displays the current version of your system's GNU Bash shell program.**

You can gracefully exit out of each subshell by entering the **exit** command:

```
$ ps -f
UID        PID PPID C STIME TTY        TIME CMD
christi+  7650 7649 0 16:01 pts/0    00:00:00 -bash
christi+  7687 7650 0 16:02 pts/0    00:00:00 bash
christi+  7709 7687 0 16:02 pts/0    00:00:00 bash
christi+  7731 7709 0 16:02 pts/0    00:00:00 bash
christi+  8081 7731 0 16:35 pts/0    00:00:00 ps -f
$
$ exit
exit
$
$ ps --forest
  PID TTY          TIME CMD
 7650 pts/0    00:00:00 bash
 7687 pts/0    00:00:00 \_ bash
 7709 pts/0    00:00:00   \_ bash
 8081 pts/0    00:00:00     \_ ps
$
$ exit
exit
$ exit
exit
$
```