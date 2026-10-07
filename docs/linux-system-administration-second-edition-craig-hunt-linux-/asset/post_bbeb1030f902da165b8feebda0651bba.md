
## Listing 7.5: Partial Output from the ps -aux Command

```
root 4270 0.0 0.8 2212 1120 pts/2 S 20:58 0:00 login - user
user 4271 0.1 0.8 1760 1032 pts/2 S 20:58 0:00 -bash
user 4301 0.1 0.6 1708 848 pts/2 S 21:00 0:00 vi todo
```

You can see in Listing 7.5 that a login process with a PID of 4270 was started for the user user; logins are always owned by root. Since it has a pts number, it is a remote login. This login process forked off a child process with a PID of 4271. This child process is the bash shell that was initiated by the login process when the user logged in.

Since user logged in remotely, a pts was assigned instead of a tty number. In old versions of Red Hat, remote tlys are referred to as tty0, tty1, etc. In Red Hat 6.0 and later, remote tlys are referred to as pts/0, pts/1, etc. The init process runs as long as the system is active. Nothing else can run without the parent init process. We introduced the init process in Chapter 3 when we discussed system startup and shutdown. You'll remember that during a system shutdown, init performs the reverse of its bootup procedure. It kills all other running processes, unmounts all filesystems, and stops the processor, along with anything else it has been configured to do.

## Managing Processes

Part of your responsibility as system administrator is to manage the system's processes to prevent a runaway process (one that has started consuming system resources far beyond what it should) from causing your system to crash. You need to understand how to obtain information about the processes that are running. We have looked at a couple of examples of the ps command to illustrate earlier points. Now we'll look at ps more formally. The ps (process status) command is the most often used method of obtaining data about current processes. The ps command called without arguments will display all of the processes running from that specific login including their PIDs, tty information, CPU time, and the command that started the process. The ps command becomes more useful if you add some arguments, as you can see in Listing 7.6.

## Listing 7.6: Output from the ps -e Command

```
PID TTY TIME CMD
1 ? 00:00:09 init
2 ? 00:00:22 kflushd
3 ? 00:00:17 kupdate
4 ? 00:00:00 kiord
5 ? 00:00:20 kswapd
6 ? 00:00:00 mdrecoveryd
296 ? 00:00:00 ppp-watch
365 ? 00:00:00 portmap
3653 tty2 00:00:00 vmware
3654 tty2 00:00:05 vmware
3655 tty2 00:00:01 vmware
3864 tty2 00:00:41 ld-linux.so.2
3887 tty2 00:00:00 netscape-commun
3946 ttyS1 00:00:00 pppd
4024 tty2 00:00:01 kvt
4025 pts/1 00:00:00 bash
4269 ? .in.rlogind
4270 pts/2 00:00:00 login
4271 pts/2 00:00:00 bash
4301 pts/2 00:00:00 vi
4317 pts/0 00:00:00 man
4318 pts/0 00:00:00 sh
4319 pts/0 00:00:00 sh
4322 pts/0 00:00:00 groff
4323 pts/0 00:00:00 less
4326 pts/0 00:00:00 grotty
4328 pts/1 00:00:00 ps
```

You can see that the output from ps -e gives you the basic information about all the running processes. The output includes the PID, the tty, the time, and the command itself. This is quite sufficient when you are trying to obtain the PID of a process to kill it or restart it.

The output from ps -au, as shown in Listing 7.7, displays information in a user-oriented format (u) that includes all processes on this terminal, including those of other users.

## Listing 7.7: Output from the ps -au Command

```
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
user 4025 0.0 0.7 1760 988 pts/1 S 18:17 0:00 bash
user 4331 0.0 0.6 2532 884 pts/1 R 21:32 0:00 ps au
```

System administrators more often use a version of the ps command that gives this information for all the processes on this terminal as well as all daemon processes, such as the ps -aef command illustrated in Listing 7.8.

## Listing 7.8: Output from the ps -aef Command

```
UID PID PPID C STIME TTY TIME CMD
root 1 0 0 Sep28 ? 00:00:09 init [3]
root 2 1 0 Sep28 ? 00:00:22 [kflushd]
root 3 1 0 Sep28 ? 00:00:17 [kupdated]
root 4 1 0 Sep28 ? 00:00:00 [kpiod]
root 5 1 0 Sep28 ? 00:00:20 [kswapd]
root 6 1 0 Sep28 ? 00:00:00 [mdrecoveryd]
bin 365 1 0 Sep28 ? 00:00:00 portmap
root 381 1 0 Sep28 ? 00:00:00 [apmd]
root 434 1 0 Sep28 ? 00:00:00 syslogd -m 0
root 445 1 0 Sep28 ? 00:00:00 klogd
daemon 461 1 0 Sep28 ? 00:00:00 /usr/sbin/atd
root 477 1 0 Sep28 ? 00:00:00 crond
root 493 1 0 Sep28 ? 00:00:00 inetd
root 509 1 0 Sep28 ? 00:00:00 [lpd]
```

This form of the command is very useful when you are looking for information on a specific daemon. Simply pipe the command into a grep command to see whether the daemon in question is running. This is especially useful in a script where the other output would confuse the situation. For this reason, it is one of the versions of the ps command that is most commonly used by system administrators. The man page for the ps command lists the many options available to tailor the output to what you need.

The command top uses the /proc filesystem to display all active processes along with the percentage of CPU power and percentage of memory that each one is using. You can also do this with a ps command, but top is better in that it is a continuous listing that is updated in real-time in order by CPU usage and is configurable. If you prefer a more visually pleasing version, try GTK/Gnome Top, found in most Linux distributions or available from http://www.tucows.com/. The most CPU-intensive programs are listed first, as shown in Figure 7.1. This is extremely helpful when your system is running slowly, and you want to find out which process is dominating the CPU. In the case of Figure 7.1, one process (gnp) is consuming 91% of the CPU time. This might or might not be a sign of trouble, depending upon whether that process *should* be consuming a lot of CPU time. The top command also lists specifics such as uptime, the number of users, the number of processes and their status, and how much real memory and swap space are being used.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_192_0.png)

Figure 7.1: Sample output of top command

### Terminating/Restarting with the *kill* Command

You know how to see what processes are dominating your CPU and slowing down your system, but what do you do about it? To terminate a process on a Linux system (and in most other Unix-like systems), you use the kill command. Issued with only a process ID as an argument, the kill command will send a signal to the process telling it to terminate. Some processes are able to catch the signal and cannot be killed so easily—the "John Wayne" processes, which simply ignore the kill signal. For these you must use a -9 argument, making the command look like this:

```
$ kill -9 234
```

The -9 cannot be caught, so the process whose ID is specified will terminate. It’s generally a good idea to try issuing the kill command *without* the -9 argument first, because some programs close themselves more cleanly this way, without leaving behind temporary files and so on.

If you need to restart a daemon, because it is hung up or because you’ve made a configuration file change, you can do this by entering the kill command with a -1 argument before the process ID, as in the example below.

```
# kill -1 234
```

Do not combine this with the -9 argument. Using `kill -1 234` will do the same thing. You may notice when you speak to other system administrators that HUP is sometimes used as a verb, basically meaning restart.

> **Note** Linux supports a command called nohup, which launches a program in such a way that it ignores the HUP kill signal. This allows you to run a program so that it survives a logout, which can be handy if you want to run a program that will be running for a very long time, but you don't want to tie up a terminal or xterm window with that program. To use this utility, just place it before an ordinary command, as in nohup number-cruncher.

## Terminating/Restarting Processes Using Scripts

In Red Hat (as in many versions of Unix), each daemon has a single script that allows you to kill it, check its status, or restart it. The handling of these scripts is based on run levels. Run levels were more thoroughly discussed in Chapter 3. For now you only need to remember that the system has several modes that can be boot into. The selection of the run level allows only certain processes to be started by the init process. On Red Hat systems, these scripts exist in the /etc/rc.d/init.d directory, one for each daemon that is to be started or shut down by the system either at bootup or run level change. Under the /etc/rc.d/ directory, there is a subdirectory for each possible run level, which contains symbolic links to the scripts that should be run for that level. Most scripts contain the capability to start, stop, status-check, and restart their specific daemons.

To kill the sendmail daemon, for instance, you use the stop option:

```
# /etc/rc.d/init.d/sendmail stop
```

An alternative method is to use the service command shorthand, which replaces the path to the service command with the word service followed by the name of the service like this:

```
# service sendmail stop
```

Whichever syntax you select, if the daemon is stopped, you'll see the message:

```
Shutting down sendmail: [OK]
```

The [OK] will be replaced by [FAILED] if the daemon was not shut down as shown below. This might happen if the daemon that you are trying to kill is not currently running.

```
Shutting down sendmail: [FAILED]
```

If you wish to start a daemon that is not currently running, substitute the word start for stop:

```
# /etc/rc.d/init.d/sendmail start
```

or

```
# service sendmail start
```

The system will then attempt to start up the sendmail daemon. A message confirming the successful startup will be displayed.

```
Starting sendmail: [OK]
```
