into more human-readable formats. The /proc file system is beyond the scope of this book, but if you want to get a better idea of what it contains you should head on over to http://en.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html for an excellent and very in-depth guide.

Processes can also be controlled at the command line, which is important because you might sometimes have only a command-line interface. Whenever an application or command is launched, either from the command line or a clicked icon, the process that comes from the kernel is assigned an identification number called a process ID or PID for short. This number is shown in the shell if the program is launched via the command line.

```
$ gedit &
```

```
[1] 6193
```

In this example, gedit has been launched in the background, and the (bash) shell reported a shell job number ([1] in this case). A job number or job control is a shell-specific feature that allows a different form of process control, such as sending or suspending programs to the background and retrieving background jobs to the foreground (see your shell's man pages for more information if you are not using bash).

The second number displayed (6193 in this example) represents the process ID. You can get a quick list of your processes by using the ps command like this:

```
# ps
PID TTY      TIME CMD

6176 pts/0    00:00:00 bash

6193 pts/0    00:00:00 gedit

6197 pts/0    00:00:00 ps
```

Note that not all output from the display is shown here. But as you can see, the output includes the process ID, abbreviated as PID, along with other information, such as the name of the running program. As with any Unix command, many options are available; the proc man page has a full list. A most useful option is aux, which provides a friendly list of all the processes. You should also know that ps works not by polling memory, but through the interrogation of the Linux /proc or process file system. (ps is one of the interfaces mentioned at the beginning of this section.)

The /proc directory contains quite a few files—some of which include constantly updated hardware information (such as battery power levels, and so on). Linux administrators often pipe the output of ps through a member of the grep family of commands to display information about a specific program, perhaps like this:

```
$ ps aux | grep gedit
andrew  6193  0.4  1.4 42772 14992 pts/0    S  20:27  0:00 gedit
```