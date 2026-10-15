
R+ state is a foreground process that is ready to run and is waiting to be scheduled to use the CPU. We discuss foreground and background processes in detail in Section 10.6.

The ps -u command shows the long listing of all the processes belonging to the user running the command. VSZ is the virtual size of the process and RSS (resident set size) is the real size of the process in memory. Both sizes are in kilobytes. Note that sarwar has logged in on five different terminals with five login C shells running.

```
% ps -u
USER       PID %CPU %MEM    VSZ   RSS TT  STAT STARTED      TIME COMMAND
sarwar 37838  0.0  0.1 25548 3900  1  Is+   6:15AM  0:00.20 -csh
(csh)
sarwar 41937  0.0  0.1 25548 3900  3  Is+   7:06AM  0:00.20 -csh
(csh)
sarwar 41985  0.0  0.1 25548 3576  4  Is+   7:07AM  0:00.10 -csh
(csh)
sarwar 44387  0.0  0.1 25548 3940  5  Ss    7:38AM  0:00.50 -csh
(csh)
sarwar 44716  0.0  0.1 16592 2304  5  R+    7:41AM  0:00.02 ps -u
sarwar 44428  0.0  0.1 25548 3900  6  Is    7:38AM  0:00.18 -csh
(csh)
sarwar 44675  0.0  0.1 16992 2800  6  I+    7:40AM  0:00.06 /bin/sh
/usr/bin/man
sarwar 44688  0.0  0.1 14788 2632  6  S+    7:40AM  0:00.03 more
%
```

You can specify a comma-separated list of UIDs to display the same information about the processes belonging to them, as in ps -u 1004,1009,1020. As a reminder, UID is the third field of a line in the /etc/passwd file. Note that the state of the first three processes is Is+, which means that they are foreground idle session leader processes. In other words, they are foreground login shell processes that have not used the CPU for over 20 seconds.

You can use the -U option on PC-BSD and Solaris to display the default status of all the processes belonging to the users whose comma-separated usernames are specified after the option. In the following example, all the processes belonging to the user sarwar are displayed. The ps -U john,davis,goldman,ibraheem command displays the default status of all the processes belonging to the users john, davis, goldman, and ibraheem.

```
% ps -U sarwar
  PID TT  STAT      TIME COMMAND
 4964  -  I    0:00.04 sshd: sarwar@pts/1 (sshd)
 8980  -  S    0:00.29 sshd: sarwar@pts/2 (sshd)
 4967  1  Is+   0:00.17 -csh (csh)
 8983  2  Ss    0:00.37 -csh (csh)
13011  2  R+    0:00.02 ps -U sarwar
%
```

You can also use the comma-separated list of UIDs of the users to display the same information. Thus, the ps -U 1004 command displays the default status of all the processes belonging to the user with UID 1004. Similarly, the ps -U 1004,1005,1001 command displays the default status of all the processes belonging to the users with UIDs 1001, 1004, and 1005.

You can use the -a and -x options to display information about your processes, processes belonging to other users, system processes, and processes not attached to any controlling terminals, such as daemons. You can determine the total number of processes, including all system processes and daemons, running on a PC-BSD system by using the ps -ax | wc -l command. The output contains a header line and a line each for the ps -ax and wc -l processes. Thus, 130 processes are currently running on our PC-BSD system if we do not count the two processes created due to the command line itself.

```
% ps -ax | wc -l
    133
%
```

You can determine the number of processes running on a Solaris machine by using the ps -e | wc -l command.

You can use the -H option to display the kernel-visible threads, known as lightweight processes (LWPs) in Solaris, in the processes running on your system. The output of the ps -axH | wc -l command shows 506 as its output. Out of these 506 lines, one line is for the output header and one line each for the ps -axH and wc -l commands each. Thus, 503 kernel-visible threads are running in the 130 processes that are currently running on the system.

```
% ps -axH | wc -l
    506
%
```

Whereas the -j, -l, -u, and -v options allow you to display the values of predetermined keywords in a known order and the standard header information, the -O and -o options allow you to display customized output: values of the keywords of your choice, in the order of your liking, and with the header of your taste. In the following session, we show the use of the ps command with these options. The keywords dsiz, ssiz, and tsiz are, respectively, the sizes (in kilobytes) of the data, stack, and text/code segments of the memory image of the process. wchan is the event a process is waiting for. The last command in the sessions shows how you can customize the header of the output.

```
% ps -O dsiz,ssiz,tsiz,vsz,rss,wchan
PID DSIZ SSIZ TSIZ  VSZ  RSS  WCHAN TT  STAT    TIME COMMAND
```
