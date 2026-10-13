This runs the uname command with three options -s, -r, and -v (these can be combined as -srv, as this example shows). The -s option causes uname to print the name of the kernel, -r prints the kernel release number, and -v prints the kernel version number. The command generates the following output on one of my Linux systems:

```
```text
Linux 2.6.13-8-default #1 Tue Sep 6 12:59:22 UTC 2005
```
```

In this case, the system is running Linux kernel version 2.6.13.

To read a file, use the more command. Here’s an example that displays the contents of the /etc/passwd file:

```
```text
more /etc/passwd

root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
... lines deleted ...
```
```

To see a list of all the programs currently running on the system, use the ps command, like this:

```
```text
ps ax
```
```

The ps command takes many options, and you can provide these options without the usual dash (-) prefix. This example uses the a and x options — the a option lists all processes that you are running, and the x option displays all the rest of the processes. The net result is that ps ax prints a list of all processes running on the system, as shown in the following sample output:

```
```text
  PID TTY          STAT     TIME COMMAND
    1 ?             S       0:01 init [5]
    2 ?             SN      0:10 [ksoftirqd/0]
    3 ?             S<      0:00 [events/0]
    4 ?             S<      0:00 [khelper]
    9 ?             S<      0:00 [kthread]
   19 ?             S<      0:00 [kacpid]
   75 ?             S<      0:02 [kblockd/0]
... lines deleted ...
```
```

Amazing how many programs can run on a system even when only you are logged in as a user, isn’t it?

As you can guess, you can do everything from a shell prompt, but it does take some getting used to.