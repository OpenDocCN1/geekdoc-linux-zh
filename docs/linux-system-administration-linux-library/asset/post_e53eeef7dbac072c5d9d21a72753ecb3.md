
# Processes

the necessary daemons, and doing whatever else it has been configured to do. Chapter 5 shows how to configure the init process.

When a parent process dies before all of its child processes have died, the remaining child processes are said to be orphan processes. These processes are required to have a parent process, so the init process adopts the orphan processes until they, too, are completed or killed.

Listing 3.5 illustrates what happens when a user logs in to your system. Earlier in the chapter we saw out from the ps -ajx command. This time we use the -aux-parameter, which displays the user who owns the process, the process ID, the percentage of CPU that this process is consuming, the amount of memory that this process is consuming, and the time process started.

# Listing 3.5 Output from the ps -aux Command

| | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---| |
| root | 4270 | 0.0 | 0.8 | 2212 | 1120 | pts/2 S | 20:58 | 0:00 | login - user |
| user | 4271 | 0.1 | 0.6 | 1760 | 1032 | pts/2 S | 20:58 | 0:00 | -bash |
| user | 4301 | 0.1 | 0.6 | 848 | | pts/2 S | 21:00 | 0:00 | vi todo |

You can see in Listing 3.5 a login process with a PID of 4270 was started for the user; logins are owned by root. Since it has a pts number, it is a remote login. This login process forked a child process with a PID of 4271. This child process is bash shell that initiated by the login process when the user logged in.

Since user logged remotely, a pts was assigned instead of a tty number. In older versions of Red Hat, remote tys are referred to as tty0, tty1, etc. In Red Hat 6.0 and later, remote tys are referred to as pts/0, pts/1. The init process runs as long as the system is active. Nothing else can run without the init process. We will discuss the init process in Chapter 5 when we discuss startup and shutdown. During a system shutdown, init performs the reverse of its bootup procedure. It kills all other running processes, unmounts all filesystems, and stops the process, along with anything it has been configured to do.

# Managing Processes

Part of your responsibility as system administrator is to manage the system's processes to prevent a runaway process (one that has started consuming system resources far beyond what it should) from causing your system to crash. You need to understand how to obtain information about the processes that are running. We have looked at a couple of examples the ps command to illustrate earlier points. Now we'll look at ps more formally. The ps (process status) command is the most often used without arguments will display all of the processes running from that specific login including the PIDs, tty information, CPU time,

![](img/4fb617eb648f87def380ef5d92052d01_106_0.png)

and the command that started the process. The ps command becomes more useful if you add some arguments, as you can see in Listing 3.6.

# Listing 3.6 Output from the ps -e Command

| PID | TTY | TIME | CMD |
|---|---|---|---|
| 1 | ? | 00:00:09 | init |
| 2 | ? | 00:00:22 | kflushd |
| 3 | ? | 00:00:17 | kupdate |
| 4 | ? | 00:00:00 | kpiod |
| 5 | ? | 00:00:20 | kswapd |
| 6 | ? | 00:00:00 | mdrecoveryyd |
| 296 | ? | 00:00:00 | ppp-watch |
| 365 | ? | 00:00:00 | portmap |
| 3653 | tty2 | 00:00:00 | vmware |
| 3654 | tty2 | 00:00:05 | vmware |
| 3655 | tty2 | 00:00:01 | vmware |
| 3864 | tty2 | 00:00:41 | ld-linux.so.2 |
| 3887 | tty2 | 00:00:00 | netscape-commun |
| 3946 | ttyS1 | 00:00:00 | pppd |
| 4024 | tty2 | 00:00:01 | kvt |
| 4025 | pts/1 | 00:00:00 | bash |
| 4269 | ? | 00:00:00 | in.rlog |
| 4270 | pts/2 | 00:00:00 | login |
| 4271 | pts/2 | 00:00:00 | bash |
| 4301 | pts/2 | 00:00:00 | vi |
| 4317 | pts/0 | 00:00:00 | man |
| 4318 | pts/0 | 00:00:00 | sh |
| 4319 | pts/0 | 00:00:00 | sh |
| 4322 | pts/0 | 00:00:00 | groff |
| 4323 | pts/0 | 00:00:00 | less |
| 4326 | pts/0 | 00:00:00 | grotty |
| 4328 | pts/1 | 00:00:00 | ps |

You can see that the output ps -e gives you basic information about all the running processes. The output includes the PID, the tty, the time, and the command. This is quite sufficient when you are trying to obtain the PID of a process to kill it or restart. The output from ps -au, as shown in Listing 3.7, displays information in a user-oriented format (u) that includes all processes on this terminal, including those of other users.

# Listing 3.7 Output from the ps -au Command

```
USER PID %CPU %MEM VSZ RSS TTY STAT START COMMAND
user 4025 0 0.7 1760 988 pts/1 S 18:17 0:00 ps
user 4331 0 0.6 2532 884 R 21:32 0:00 ps
```

System administrators more often use a version of the ps command that gives information for all processes on this terminal as well as daemon processes, such as the ps -aef command illustrated in Listing 3.8.

# Listing 3.8 Output from the ps -aef Command

| UID PPID C STIME TTY TIME CMD |
|---|---|---|---|---|---|---|
| root | 1 | 0 | Sep 28 | ? | 00:00:09 | init |
| root | 2 | 1 | Sep 28 | ? | 00:00:22 | kflushd |
| root | 3 | 1 | Sep 28 | ? | 00:00:17 | kupdate |
| root | 4 | 1 | Sep 28 | ? | 00:00:00 | kpiod |
| root | 5 | 1 | Sep 28 | ? | 00:00:20 | kswapd |
| root | 6 | 1 | Sep 28 | ? | 00:00:00 | mdcoveryyd |
| bin | 365 | 1 | Sep 28 | ? | 00:00:00 | portmap |
| root | 381 | 1 | Sep 28 | ? | 00:00:00 | apmd |
| root | 434 | 1 | Sep 28 | ? | 00:00:00 | syslog -m |
| root | 445 | 1 | Sep 28 | ? | 00:00:00 | klogd |
| daemon | 461 | 1 | Sep 28 | ? | 00:00:00 | /usr/sbin/atd |
| root | 477 | 1 | Sep 28 | ? | 00:00:00 | crond |
| root | 493 | 1 | Sep 28 | ? | 00:00:00 | inetd |
| root | 509 | 1 | Sep 28 | ? | 00:00:00 | lpd |

![](img/4fb617eb648f87def380ef5d92052d01_108_0.png)

# Chapter 3 Linux Files and Processes

This form of the command is very useful when you are looking for information on a specific daemon. Simply pipe the command into a grep command to see whether the daemon is in question. This is especially useful in a script where the other output would confuse the situation. For this reason, it is one of the ps command that most commonly used by system administrators. The man page for the ps command lists the many options available to tailor the output to what you need.

The top command uses the /proc system to display all processes with the percentage of CPU and percentage of memory that each one is using. You can also do this with a ps command, but top is better in that it is a continuous listing which is updated in real-time by CPU usage and is configurable. The most CPU-intensive programs are listed first, as shown in Figure 3.3. This is extremely helpful when your system is running slowly, and you want to find out process is dominating the CPU. In the case of Figure 3.3, one process (setathom) is consuming 97.8% of the CPU time. This might or might not be a sign of trouble, depending upon process should be consuming a lot of CPU time. The top command also lists such as uptime, the number of users, the number of processes and their status, and how real memory and space are used.

Figure 3.3 Sample output of top command

![](img/4fb617eb648f87def380ef5d92052d01_109_0.png)

| PID | USER | NI | VIRT | RES | SHR | S | %CPU %MEM | TIME | COMMAND |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---|
| 1063 | root | 19 | 15332 | 140 | 800 | R | 12.0 | 2:07 | setathom |
| 959 | root | 20 | 12772k | 10872k | 19000 | S | 0.9 | 0:04 | X |
| 1 | root | 0 | 17136 | 1718 | 748 | R | 1.5 | 0:15 | os |
| 1115 | demithad | 0 | 10444 | 816 | | | | | |
| 1013 | demithad | 0 | 15638k | 3276 | | | | | |
| 1 | root | 0 | 536 | 536 | 468 | S | 0.0 | 0:04 | init |
| 2 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | kflushd |
| 3 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | update |
| 4 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | kpidod |
| 5 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | kswad |
| 6 | root | -20 | -20 | 0 | 0 | S | 0.0 | 0:00 | rcreceiver |
| 63 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | khubd |
| 292 | root | 0 | 784 | 784 | 660 | S | 0.6 | 0:00 | pum |
| 245 | root | 0 | 612 | 612 | 512 | S | 0.0 | 0:04 | ppage |
| 385 | root | 0 | 836 | 836 | 464 | S | 0.6 | 0:06 | klogd |
| 370 | root | 0 | 576 | 576 | 484 | S | 0.4 | 0:04 | portnap |
| 388 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | lockd |
| 387 | root | 0 | 0 | 0 | 0 | S | 0.0 | 0:00 | rpcbind | |
