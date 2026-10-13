
![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_481_0.png)

Be careful about deleting files with file-number extensions, such as .1, across your system: You will delete a lot of libraries and manual pages if you automate a search-and-destroy mission starting at the root, or /, directory.

If you feel uncomfortable with letting the find command run through your file system and deleting files, have the command generate a report of candidate files as follows:

```
# find / \( -name core -o -name *.o \) -xdev > deletelist.txt
```

Note that you can also set this command to run unattended, at regular intervals, and have the report emailed to you as an automatic reminder. See Hour 24, “Using Scheduling to Automate System Management,” for details.

If you experiment with your own combination of commands, you’ll soon design your own customized reports and cleanup actions. You now know how to get information about your drive space. You’ll also learn about managing disk space, using quotas (software limits on hard drive usage) in the section “Managing User Access” later in this chapter. For now, you’ll learn how to find out more about what’s going on in your computer’s memory when you run Linux.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_481_1.png)

Compressing unused files or directories or archiving and then deleting these directories is another way to conserve disk space. See Hour 5, “Manipulation and Searching Commands” for information about using compression utilities. Also, see Hour 23, “Backing Up and Restoring Your System” for details about backing up or restoring OpenLinux files and directories.

## Getting Memory Information

New Term Although the industry trend has been to offer more hard drive space and more system memory, or RAM, for less money, many people don’t like to outlay more cash to expand their systems. The good news is that Linux is efficient at using memory because even a 16MB system provides enough room (with an equal amount of swap space) to run X11 and most programs well. The bad news is that programs are getting larger all the time, especially with feature creep, in which more and more functions creep into programs. (This is true of the Linux kernel, which has tripled in size over the past few years.) This section introduces you to some programs you might find helpful in understanding your system’s memory and gives you some tips on conserving memory.

### Memory Reporting with the free Command

The free command shows breakdowns of the amounts and totals of free and used memory, including your swapfile usage. This command, in the /usr/bin directory, has several command-line options, but is easy to run and understand:

```
# free
Mem: total used free shared buffers cached
63136 60064 3072 53664 11080 26992
-/+ buffers/cache: 21992 41144
Swap: 130748 2616 128132
```

This shows a system with 64MB RAM and 131MB of swap space. Notice that nearly all the system memory is being used (normal) and almost 3MB of swap space (great!) has been used.

By default, the free command displays memory in kilobytes, or 1024-byte notation. You can use the -b option to display your memory in bytes or the -m option to display memory in megabytes. You can also use the free command to constantly monitor how much memory is being used through the -s command. This is handy as a real-time monitor if you specify a 0.1-second update and run the free command in a terminal window under X11. For example, to monitor your disk space in an X11 terminal window, use the free command like so:

```
# /usr/bin/free -b -s1
```

This will print a scrolling report, updated each second, in your terminal window.

### Virtual Memory Reporting with the vmstat Command

The vmstat command, found under the /usr/bin directory, is a general-purpose monitoring program, which offers real-time display of not only memory usage and virtual memory statistics, but also disk activity, system usage, and central processing unit (CPU) activity. If you call vmstat without any command-line options, you'll get a one-time snapshot:

```
# vmstat
procs memory swap io system cpu
r b w swpd free buff cache si so bi bo in cs us sy id
0 0 0 7468 1060 4288 16552 1 1 10 1 134 68 3 2 96
```

The major types of activity reported by vmstat are processes (procs), memory (in kilobytes), swap space (in kilobytes), input/output from block devices (hard drives), system interrupts (number per second), and percentages of central processing unit (CPU) time spent on users, the system, and idling.

If you specify a time interval in seconds on the vmstat command line, you'll get a continuously scrolling report. Having a constant display of what is happening with your computer can help you if you're trying to find out why your computer suddenly slows down or why there's a lot of disk activity.

### Viewing Your Shell's “Ulimit”ations

You've already seen how you can limit the size of core dump files in this hour. There are other settings you can set in your shell. If you're using the bash or pdksh (ksh) shell, you can use the ulimit command's -a option to print your current settings:

```
# ulimit -a
core file size (blocks)       0
data seg size (kbytes)        unlimited
file size (blocks)            unlimited
max memory size (kbytes)      unlimited
stack size (kbytes)           8192
cpu time (seconds)            unlimited
max user processes            256
pipe size (512 bytes)         8
open files                    256
virtual memory (kbytes)       2105343
```

If you're using the tcsh or csh shell, you can use the limit command to list the current settings:

```
$ limit
cputime               unlimited
filesize              unlimited
datasize              unlimited
stacksize             8192 kbytes
coredumpsize          0 kbytes
memoryuse             unlimited
descriptors           256
memorylocked          unlimited
maxproc               256
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_483_0.png)

These limits are different from limits for the root operator. The limits shown in this example are known as soft limits (limits that may be changed by any user).

To view the shell's hard limits (limits that may only be raised by root), log in as the root operator, and use the -a limit option (use -Ha for bash or ksh's ulimit command):

```
$ su
Password:
# limit -h
cputime               unlimited
filesize              unlimited
datasize              unlimited
stacksize             8192 kbytes
coredumpsize          unlimited
memoryuse             unlimited
descriptors           256
memorylocked          unlimited
maxproc               256
```

As you can see, viewing the limits as the root operator in the tcsh shell shows a much different situation. This is another good reason not to run as the root operator. As a sysadmin, you can use these settings to limit the amount of memory or number of processes available to each user. This is extremely handy if you have a number of people working on your computer at the same time and you want to conserve system memory. For using Linux on a standalone computer under your normal login and working conditions, you'll find the default limits quite reasonable.

### Reclaiming Memory with the kill Command

As a desperate measure if you need to quickly reclaim memory, you can stop running programs using the kill command. To kill a specific program, you should use the ps command to list current running processes and then stop any or all of them with the kill command. By default, the ps command lists processes that you own and you can kill:

```
# ps
PID TTY STAT TIME COMMAND
367 p0 S 0:00 bash
581 p0 S 0:01 rxvt
582 p1 S 0:00 (bash)
747 p0 S 0:00 (aplix)
809 p0 S 0:18 netscape.index.html
810 p0 S 0:00 (dns helper)
945 p0 R 0:00 ps
```

The ps command will list the currently running programs and the program's process number, or PID. You can use this information to kill a process with the -9, or SIGKILL signal:

```
# kill -9 809
```

However, if you need to reclaim memory efficiently, you should use the ps command's m option, which also lists the memory usage of each process:

```
# ps m
PID TTY MAJFLT MINFLT TRS DRS SIZE SWAP RSS SHRD LIB DT
COMMAND
747 p0 0 3 16 208 364 140 224 224 0 0
(aplix)
582 p1 151 274 124 184 436 128 308 268 0 10
(bash)
959 p0 89 20 28 376 404 0 404 320 0 21 ps m
```
