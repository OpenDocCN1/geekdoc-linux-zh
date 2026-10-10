# Part I: The Linux Command Line

Unfortunately, with this robustness comes complexity—in the form of numerous parameters— making the ps command probably one of the most difficult commands to master. Most system administrators find a subset of these parameters that provide the information they want and then stick with using only those.

That said, however, the basic ps command doesn’t provide all that much information:

```
$ ps
PID TTY TIME CMD
3081 pts/0 00:00:00 bash
3209 pts/0 00:00:00 ps
$ 
```

Not too exciting. By default the ps command shows only the processes that belong to the current user and that are running on the current terminal. In this case, only the Bash shell was running (remember, the shell is just another program running on the system) and, of course, the ps command itself.

The basic output shows the process ID (PID) of the programs, the terminal (TTY) that they are running from, and the CPU time the process has used.

> **NOTE**
> The tricky feature of the ps command (and the part that makes it so complicated) is that at one time there were two versions of it. Each version had its own set of command-line parameters controlling what information it displayed and how. Recently, Linux developers have combined the two ps command formats into a single ps program (and of course added their own touches).

The GNU ps command that’s used in Linux systems supports three types of command-line parameters:

+   - UNIX-style parameters, which are preceded by a dash
+   - BSD-style parameters, which are not preceded by a dash
+   - GNU long parameters, which are preceded by a double dash

The following sections examine the three different parameter types and show examples of how they work.

# UNIX-style parameters

The UNIX-style parameters originated with the original ps command that ran on the AT&T UNIX systems invented by Bell Labs. These parameters are shown in Table 4.1.