
## Finding Out What Processes Are Running with ps

The jobs that you've been talking about so far are actually types of processes. Processes are programs, scripts, or commands—including anything you do in the Unix system. All jobs are processes, but not all processes are jobs.

Occasionally, you may want to find out what processes are running on the Unix system. You can do this using ps, as shown in Code Listing 9.12.

### To find out what processes are running with ps:

- ps

At the shell prompt, type ps to see the list of the current processes that you're running in your current shell, including processes for your current shell, as well as any other jobs (Code Listing 9.12).

The exact information you see will vary from system to system. In general, though, you'll find the PID (process identification) number at the far left and the process name at the right.

```
[jdoe@frazz jdoe]$ ps
PID TTY TIME CMD
21016 pts/22 00:00:00 bash
21707 pts/22 00:00:00 ps
[jdoe@frazz jdoe]$ ps -a
PID TTY TIME CMD
21407 pts/3 00:00:00 su
21411 pts/3 00:00:00 bash
21441 pts/3 00:00:00 su
21444 pts/3 00:00:00 bash
19274 pts/11 00:00:05 xterm
23357 pts/12 00:00:04 xterm
13369 pts/5 00:00:00 zsh
23815 pts/9 00:00:00 su
23818 pts/9 00:00:00 bash
23878 pts/9 00:00:00 csh
23942 pts/9 00:00:01 ssh
23972 pts/18 00:00:00 su
23975 pts/18 00:00:00 bash
24103 pts/5 00:00:00 ssh
4658 pts/15 00:00:11 ssh
24318 pts/8 00:00:01 xterm
29188 pts/4 00:00:00 rxvt-2.7.9
29368 pts/4 00:00:00 rxvt
29440 pts/8 00:00:00 vi
23883 pts/20 00:00:02 xterm
27257 pts/16 00:00:01 ssh
6804 pts/20 00:00:00 xterm
26531 pts/20 00:00:02 xterm
21813 pts/22 00:00:00 su
21016 pts/22 00:00:00 bash
21708 pts/22 00:00:00 ps
[jdoe@frazz jdoe]$
```

Code Listing 9.12 Using ps, you can find out what processes are currently running.

## Tips

- You can find out what processes other people are running by typing `ps -a` at the shell prompt and what processes the system is running (also called daemons) with `ps -ax`. The `ps -ef` variant is usually pretty useful for us.
- You can sometimes, depending on the system, get a broader look at currently running processes by typing `ps -a -f`. The `f` flag indicates “forest” view, which lets you see not only the processes, but also how they relate to each other, as shown in **Code Listing 9.13**.
- The results `ps` offers vary greatly depending on the Unix flavor you’re using. Type `man ps` at the shell prompt to find out more about your specific `ps` capabilities.

```
$ ps -a -forest
  PID TT  STAT TIME COMMAND
15043 p0  S     0:00 /bin/login -h calvin.raycomm.com -p
15044 p0  0:01  \_ -bash
16344 p0  T N 0:00  \_ sh ./slowscript
16345 p0  T N 0:00      \_ sleep 50
16449 p0  R     0:00      \_ ps f
15911 p1  S     0:00 /bin/login -h calvin.raycomm.com -p
15912 p1  S     0:01  \_ -bash
16216 p1  T     0:00      \_ telnet
16217 p1  T     0:00      \_ lynx http://www.raycomm.com/
16267 p1  T     0:00      \_ man telnet
16268 p1  T     0:00          \_ sh -c (cd /usr/man ; (echo -e '.pl 1100i'; cat
16269 p1  T     0:00              \_ sh -c (cd /usr/man ; (echo -e '.pl 1100i'; cat
16270 p1  T     0:00                  \_ sh -c (cd /usr/man ; (echo -e '.pl 1100i'; cat /usr/man/man1/telnet.1
16271 p1  T     0:00                      \_ /usr/bin/gtbl
16272 p1  T     0:00                      \_ sh -c (cd /usr/man ; (echo -e '.pl 1100i'
$
```

**Code Listing 9.13** The forest view gives you a broader look at running processes.

## Deleting Processes with kill

In addition to suspending jobs and running them in the foreground and background, you can also choose to just delete them completely. For example, you might realize midway through a job that you goofed and need to redo it. Or perhaps you’ve accessed and suspended a man page and no longer need to reference it.

Using kill, you can delete essentially any process running or suspended on the Unix system. As Code Listing 9.14 shows, you delete a process by first listing the processes, then using the kill command.

### To kill a job with kill:

1. jobs
   At the shell prompt, type jobs, then note the number or name of the job you want to kill.
2. kill %ftp
   In most shells, you can kill jobs with kill followed by %, and the job number or command name—for example, you could kill an ftp job with a job number of 1 using kill %ftp or kill %1. If your shell doesn’t cooperate, read on.

### To delete a process with kill:

1. ps
   At the shell prompt, type ps to see the list of all your current jobs (Code Listing 9.14). Note the PID (process identification) number of the process you want to delete.
2. kill 16217
   Type kill 16217 followed by the PID number of the job you’re deleting.

```
$ ps -a -forest
PID TTY STAT TIME COMMAND
15911 p1 S 0:00 /bin/login -h calvin
  -> raycomm.com -p
15914 p1 S 0:01 _ -bash
16216 p1 T 0:00 _ telnet
16217 p1 T 0:00 _ lynx
http://www.raycomm.com/
$ kill -9 16217
$ ps -a -forest
PID TTY STAT TIME COMMAND
15911 p1 S 0:00 /bin/login -h calvin
  -> raycomm.com -p
15914 p1 S 0:01 _ -bash
16216 p1 T 0:00 _ telnet
$
```

Code Listing 9.14 Using kill plus the PID number, you can delete practically any process running or suspended on the system.

## Tips

- Occasionally, you’ll use kill and find that the process just keeps going. Try kill -9 followed by the PID number to delete the process.
- Be careful not to kill your current shell process, or you’ll abruptly find your connection broken. Doing so would be like sawing off the branch you’re sitting on.
- Many newer Unix systems allow you to use pkill to kill processes by name, not number. For example, you might use pkill ftp to kill a suspended ftp session.
