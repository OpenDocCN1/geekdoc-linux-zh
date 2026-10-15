

# SYNTAX

```
cmd1; cmd2; ...; cmdN
```

Purpose: Execute commands cmd1, cmd2, ..., cmdN sequentially as separate processes

Note that the semicolon is used as a command separator and, therefore, does not follow the last command. No spaces are needed before and after a semicolon, but you can use spaces for clarity. These commands execute one after the other, as though each were typed on a separate line. In the following session, the date and echo commands execute sequentially as separate processes. The first session is on PC-BSD running C shell and the second is on Solaris running Bash. Note the difference between the outputs of the date command on the two systems.

```
% date; echo Hello, World!
Sat Sep 20 10:27:50 PKT 2014
Hello, World!
%
$ date; echo Hello, World!
Saturday, September 20, 2014 10:29:05 PM PKT
Hello, World!
$
```

You can specify parallel execution of commands in a command line by ending each command with an ampersand (&). The commands that end with & also execute in the background. No spaces are required before or after &, but you can use spaces for clarity. When you execute a command in the background, the shell displays the following pair as output: [jobID] PID, where the first job ID is 1, increasing linearly by adding one to the last-used job ID. Like PIDs, a job ID may be recycled if it has not been assigned to a process currently. The following is a brief description of the syntax for parallel execution of shell commands specified in one command line.

# SYNTAX

```
cmd1& cmd2& ... cmdN&
```

Purpose: Execute commands cmd1, cmd2, ..., cmdN in parallel as separate processes

The following sessions were executed on PC-BSD under C shell and Solaris under Bash, respectively. The date and echo commands execute in parallel and in the background, followed by the sequential execution of the uname and who commands in the foreground. In general, since the who command executes at the end, its output is always displayed at the end. The outputs of the other three commands (date, echo, and uname) may be displayed in any order. This order is due to the scheduling of processes and the amount of time each takes to execute. Thus, the same output order may or may not be reproduced if you execute the command line again. In the following session, the outputs are displayed in the order echo, uname, date, and who for PC-BSD, and echo, date, uname, and who for Solaris. The job and process ID pairs for the date and echo commands are [1] 15167 and [2] 15168, respectively, on PC-BSD. Similarly, the job and process IDs for the date and echo commands on Solaris are [1] 6802 and [2] 6803, respectively.

```
% date& echo Hello, World!& uname; who
[1] 15167
[2] 15168
Hello, World!
FreeBSD
Sat Sep 20 10:31:51 PKT 2014
malik          pts/0        Aug 14 09:45  (:0)
sarwar         pts/1        Sep 20 10:27  (static-host202-147-168-98.link.net.pk)
[2]  + Done                     echo Hello, World!
[1]  + Done                     date
%
```

```
$ date& echo Hello, World!\& uname; who
[1] 6802
[2] 6803
Hello, World!
Saturday, September 20, 2014 03:35:57 PM PKT
SunOS
[1]- Done                     date
[2]+ Done                     echo Hello, World\!
root     console    Sep 19 17:13
sarwar   pts/1      Sep 20 15:30    (static-host202-147-168-98.link.net.pk)
$
```

The last & in a command line puts all the commands since the previous & in one process. In the following command line, therefore, the date command executes as one process and all the commands in who; whoami; uname; echo Hello, World! & as another process. The job and process ID pairs for these processes are [1] 49380 and [2] 49381, respectively, on PC-BSD.

```
% date & who ; whoami ; uname ; echo Hello, World! &
[1] 49380
[2] 49381
[sarwar@pcbsd-srv] ~/unix3e/ch10% Sat Sep 20 17:49:58 PKT 2014
malik          pts/0        Aug 14 09:45  (:0)
sarwar         pts/1        Sep 20 17:45  (182.178.199.200)
malik                 pts/2        Sep 20 10:59 (:0)
sarwar
FreeBSD
Hello, World!
<Enter>
[2]  Done             ( who; whoami; uname; echo Hello, World! )
[1]  + Done            date
%
```

As shown in the following session, when run on Solaris, the job ID and process ID pair for the two processes are [1] 7540 and [1] 7544, respectively. Note that whereas job IDs for the two jobs on PC-BSD are 1 and 2, they are 1 each on Solaris. Further, the process IDs for the two processes on PC-BSD are two consecutive numbers, whereas they are nonconsecutive on Solaris. This means that under PC-BSD, these processes were created right after each other and were assigned consecutive job IDs and consecutive process IDs. On the other hand, after the creation of the date process, three other processes with process IDs 7541, 7542, and 7543 were created before the second process in our command line was created. This explains both of our processes getting job ID 1 each. Note that we replace ! in the echo command with \! in Bash under Solaris. Finally, as shown in the shaded regions of the two sessions, since the shell prompt returns on both systems after the two processes (jobs) have been created but before any or some output has been displayed on the screen, we have to hit the <Enter> key to display the shell prompt again.

```
$ date & who; whoami; uname; echo Hello, World\! &
[1] 7540
Saturday, September 20, 2014 10:54:27 PM PKT
root        console     Sep 19 17:13
sarwar      pts/1       Sep 20 22:48     (182.178.199.200)
[1]+ Done                   date
sarwar
SunOS
[1] 7544
$ Hello, World!
<Enter>
[1]+ Done                   echo Hello, World\!
$
```

As will be discussed briefly in Chapter 12, UNIX allows you to group commands and execute them as one process by separating commands using semicolons and enclosing them in parentheses. This is called command grouping. Because all the commands in a command group execute as a single process, they are executed by the same subshell. However, all the commands execute sequentially, one after the other. The following is a brief description of the syntax for command grouping.

