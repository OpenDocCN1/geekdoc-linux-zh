
Table 9-5 explains the meaning of the common output fields for ps.

## Table 9-5 Output Fields for ps

| Field | Explanation |
|---|---|
| USER or UID | The process owner's username. |
| PID | Process ID. |
| %CPU | CPU utilization of the process. Because the time base over which this is computed varies, it is possible for this to exceed 100 percent. |
| %MEM | Percentage of memory (in kilobytes) that the process is using. |
| SIZE | Size (in kilobytes) of virtual memory that the process is using. |
| RSS | Resident Set Size – size of real memory (in kilobytes) the process is using. |
| TTY | Terminal (called tty) that is associated with the process. Usually, the tty name is shortened. For example, p7 is displayed to represent /dev/ttyp7. |
| STAT | State of the process. Process states are represented by characters such as D (disk wait); I (idle); N (lowered priority by nice); P (page wait); R (running or ready to run); S (sleeping); T (terminated); W (swapped out); Z (zombie); < (execution priority raised by superuser), and so on. |
| START | Process start time or date. |
| TIME | Total CPU time the process is using. |
| COMMAND | Command line being executed. |
| NI | The nice priority number. |
| PRI | The process's priority number. |
| PPID | The process ID (PID) of the parent process. |
| WCHAN | The name of the kernel function where a process is sleeping. This name is retrieved from the /boot/System.map file. |
| FLAGS | A numeric flag associated with the process. |

The ps utility also accepts a number of command-line arguments. Table 9-6 shows commonly used options.

## Table 9-6 Commonly Used ps Options

| Options | What It Shows |
|---|---|
| A | Processes belonging to all users. |
| E | Displays process environment information. |
| L | Displays output in long format. |
| U | Displays user name and process start time. |
| W | Displays the output in wide format. If you don't use this option, the output is truncated if it cannot fit on a line. |
| Txx | Displays processes associated with xx terminal (tty) device. |
| X | Displays processes without controlling the terminal (tty). |

To help you really see how versatile ps can be, the following sections discuss some examples of how to use some of the more common ps options together.

## Customizing your process display

Using the -a and -u options with ps tells the command to display all processes (excluding the one not associated with any controlling tty). For example, to find out what processes a particular user owns, you can run the following command, substituting username for the name of the actual user:

```
ps au | grep username
```

For example, the ps au | grep sheila command shows all the interactive processes (that is, processes associated with a tty) that are being run by user sheila. Typically, normal users are not allowed to run daemon processes or processes not associated with a tty. However, if you just want to find if any such processes exist for any user, you can run the following command:

```
ps aux
```

Adding the -x option to the -a and -u options tells ps to list processes detached from terminals. You can identify these processes by looking at the TTY field, which displays a "?" character instead of the shortened name of a tty device such as p7 (/dev/ttyp7).

## Finding the PID of a process’s parent

To find the PID of a process’s parent, you can run the following command, where PID is the process ID:

```
ps l PID
```

For example, if you want to find the parent of a process with PID 123, you can run the ps l 123 command. The parent’s PID will be listed in the PPID field of the report.

## Displaying environment information

Knowing a program’s environment information is often a great way to determine bugs and also configuration problems. To determine what initial environment variables are available to processes, you can run the following command, which appends the environment information to the COMMAND field of the resulting ps report:

```
ps e
```

![](img/9eb7e89292d2f85707b4d49102c865b7_234_0.png)

A regular (non-superuser or root) user cannot use the -e option to see the environment information of another user's processes. This is a security feature. Only root or other superusers can view environment information of all the processes.

## Monitoring a process over time

At times you find that you need to run ps to monitor a specific process for a certain amount of time. For example, say that you installed a new sendmail mail server patch and want to make sure the server is up and running and determine whether it is using an excessive amount of system resources. In such a case you can combine a few Linux commands as follows:

```
watch --interval=n "ps auxw | grep process_you_want_to_monitor"
```

For example, you can run watch --interval=30 "ps auxw | grep sendmail" to see how much resource sendmail is using by running the ps program every 30 seconds.

## Viewing processes in a tree structure

You can run pstree to display a tree structure of all processes running on your system. A sample output of the pstree command is shown below.

```
init-+-apmd
    |-atd
    |-crond
    |-identd---identd---3*[identd]
    |-kflushd
    |-khubd
    |-klogd
    |-kpiod
    |-kswapd
    |-kupdate
    |-lockd---rpciod
    |-lpd
    |-mdrecoveryd
    |-6*[mingetty]
    |-named
    |-nmbd
    |-portmap
    |-rhnsd
    |-rpc.statd
    |-safe_mysqld---mysqld---mysqld---mysqld
    |-sendmail
    |-smbd---smbd
    |-sshd-+-sshd---bash---su---bash---man---sh---sh-+-groff---
grotty
        |
        |               `-less
        |   `-sshd---bash---su---bash---pstree
    |-syslogd
    |-xfs
    `-xinetd
```

You can tell the following from the above output:

- The parent of all processes is `init`. This does not change.
- One branch of the tree is created by `safe_mysqld`, which has itself spawned three `mysqld` daemon processes.
- Another branch of the tree is the `sshd` branch. The `sshd` daemon has forked two child daemon processes that have then opened `bash` shells and launched other processes down the road. Notice that the `pstree` output was generated by one of the subbranches of the `sshd` daemon.
- The output shows that I used `sshd` to connect to my Linux system, switched to `bash` as my shell after I logged in, used `su` to switch users to root (instead of logging in directly as root, which is both risky and usually unnecessary), and then ran the `pstree` command.

## Running top to monitor system activity

The top utility allows you to monitor system activity in an interactive manner. When you run top from a shell window or an xterm it displays all the active processes and updates the screen by using a user-configurable interval. A sample top session is shown in Listing 9-1.

### Listing 9-1 An example top session

```
12:13pm up 1:15, 2 users, load average: 0.05, 0.07, 0.01

48 processes: 47 sleeping, 1 running, 0 zombie, 0 stopped

CPU states: 1.1% user, 2.1% system, 0.0% nice, 96.7% idle

Mem: 387312K av, 96876K used, 290436K free, 27192K shrd, 36040K buff

Swap: 265064K av, 0K used, 265064K free 34236K cached

PID USER PRI NI SIZE RSS SHARE STAT %CPU %MEM TIME COMMAND
6748 kabir 15 0 1032 1032 832 R 0.9 0.2 0:00 top
1 root 0 0 532 532 468 S 0.0 0.1 0:06 init
2 root 0 0 0 0 0 SW 0.0 0.0 0:00 kflushd
3 root 0 0 0 0 0 SW 0.0 0.0 0:00 kupdate
4 root 0 0 0 0 0 SW 0.0 0.0 0:00 kpiod
```

### Listing 9-1 Continued

```
5 root 0 0 0 0 0 SW 0.0 0.0 0:00 kswapd
6 root -20 -20 0 0 0 SW< 0.0 0.0 0:00 mdrecoveryd
45 root 0 0 0 0 0 SW 0.0 0.0 0:00 khubd
349 root 0 0 612 612 512 S 0.0 0.1 0:00 syslogd
359 root 0 0 480 480 408 S 0.0 0.1 0:00 klogd
374 rpc 0 0 576 576 484 S 0.0 0.1 0:00 portmap
390 root 0 0 0 0 0 SW 0.0 0.0 0:00 lockd
391 root 0 0 0 0 0 SW 0.0 0.0 0:00 rpciod
401 rpcuser 0 0 768 768 656 S 0.0 0.1 0:00 rpc.statd
416 root 0 0 524 524 460 S 0.0 0.1 0:00 apmd
470 nobody 0 0 720 720 608 S 0.0 0.1 0:00 identd
477 nobody 0 0 720 720 608 S 0.0 0.1 0:00 identd
478 nobody 0 0 720 720 608 S 0.0 0.1 0:00 identd
480 nobody 0 0 720 720 608 S 0.0 0.1 0:00 identd
482 nobody 0 0 720 720 608 S 0.0 0.1 0:00 identd
489 daemon 0 0 576 576 500 S 0.0 0.1 0:00 atd
504 named 0 0 1928 1928 1152 S 0.0 0.4 0:00 named
535 root 0 0 1040 1040 832 S 0.0 0.2 0:00 xinetd
550 root 0 0 1168 1168 1040 S 0.0 0.3 0:00 sshd
571 lp 0 0 888 888 764 S 0.0 0.2 0:00 lpd
615 root 0 0 1480 1480 1084 S 0.0 0.3 0:00 sendmail
650 root 0 0 744 744 640 S 0.0 0.1 0:00 crond
657 root 0 0 912 912 756 S 0.0 0.2 0:00 safe_mysqld
683 mysql 0 0 1376 1376 1008 S 0.0 0.3 0:00 mysqld
696 xfs 0 0 2528 2528 808 S 0.0 0.6 0:00 xfs
704 mysql 0 0 1376 1376 1008 S 0.0 0.3 0:00 mysqld
```

By default, top updates its screen every second. You can change this interval by using the d seconds option. For example, to update the screen every 5 seconds you would run the top d 5 command. If you let top update the screen every second, the program will show up as the main resource consumer in its own output. So, it’s a good idea to use a 5- or 10-second interval for the screen update interval.
