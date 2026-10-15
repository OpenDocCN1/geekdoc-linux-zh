
+   1. In the script, the first line is

```
#!/bin/csh -feb
```

The -feb options:

-   -f fast start up; don't execute .cshrc
-   -e abort immediately if interrupted
-   -b this is a setuid script

+   2. Next, change the permissions on the script so that it can run as a setuid program:

```
% chmod 4755 script_name
or
% chmod +srx script_name
% ls -l
-nwxr-xr-x 2 ellie 512 Oct 10 17:18 script_name
```

Because of the security risks involved with setuid programs, most systems will allow the administrator to disable setuid and setgid programs for individual filesystems. The UNIX find command can also be used to locate programs that are setuid to root:

```
# find / -user root -perm -4000 | more
```

Within a shell script, you can check for files that are setuid programs with the file-testing operators available for all shells. For example, Korn and Bash shells, the test would be:

```
if [[ -u filename ]]; then
```

for C/TC shell:

```
if { test -u filename } then
```

and for Bourne shell:

```
if test -u filename; then
```

or

```
if [ -u filename ]; then
```

## 16.4 Boot Scripts

During a system boot, shell scripts are run to perform tasks such as starting daemons and network services, starting database engines, mounting disks, and so on. They are also run during system shutdown. These scripts are known as boot scripts, startup and shutdown scripts, init scripts, or run control scripts, depending on which documentation you are reading and to whom you are talking. They are frequently called boot scripts, and that term will be used to refer to these scripts for the rest of the chapter. On almost all UNIX/Linux systems, the boot scripts are written in Bourne or Bash shells. A UNIX installation will come with a starter set of boot scripts so that administrators are not required to write the scripts themselves, but they should be able to debug and modify scripts when required.

For those familiar with the differences between System V and BSD-style UNIX systems, this section will focus on the System V-style boot scripts, mainly because they are the most commonly used.

### 16.4.1 A Little Terminology

Throughout this text, we have used the terms such as the kernel, init, processes, PIDs, daemons, and initialization scripts in relation to the shell. This section provides some further clarification of these terms as they relate to the boot-up process and the scripts that are started during system initialization.

### The Kernel and init.

When the system boots, the UNIX/Linux kernel is loaded from disk. It is the program that manages the operating system from boot-up to shutdown. Initially it initializes device drivers, starts the swapper, and mounts the root file system (/). The kernel then creates the first process, called init, the parent of all processes, with a PID (process identification number) number 1. When init starts, it reads from an initialization file called /etc/inittab. This file defines what processes to start during boot-up as well as during normal operation, supervises logins on serial ports, and defines run levels to determine what processes or groups of processes should be started.

### What Is a Run Level?

A run level, also called a system state, determines which set of processes are currently available on a system. Usually there are eight run levels: 0–6 and s or S. The run levels fit into three general categories: halted, single-user, and multiuser. In the halted system state, UNIX is not running—it is halted. Moving to a halted state shuts down the system. Run level 0 is a halted state. On some versions of UNIX, notably Solaris, run level 5 is also a halted state and unlike run level 0, the machine is automatically powered off after UNIX is halted. The single-user run level is either S or 1. In single-user mode, the system console is opened, and only root is logged on. (See "Single-User Mode" on page 1033.) The multiuser run levels are 2–5. The multiuser mode allows users to log into the system. The run level numbers for multiuser vary quite a bit from one version of UNIX/Linux to another. To complicate things even more, there may be more than one multiuser run level on a particular system. For example, under SuSE Linux, run levels 2 and 5 are both multiuser levels. Level 2 allows users to log in, but they will log into a text-only, single-screen session. Level 5 allows login, and additional processes are started including window managers such as KDE (the K Desktop Environment). As superuser, you can change to a different run level with the init (or telinit) command. For example init 0 would move the system into run level 0, thus shutting it down.
