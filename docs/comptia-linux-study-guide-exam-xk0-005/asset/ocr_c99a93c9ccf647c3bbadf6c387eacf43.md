Recently, the GNU developers decided to merge the two versions into a single ps program, and of course, they added some additional parameters of their own. The current ps program used in Linux supports three different styles of command-line parameters:

+   - Unix-style parameters, which are preceded by a dash
+   - BSD-style parameters, which are not preceded by a dash
+   - GNU long parameters, which are preceded by a double dash

This makes for lots of possible parameters and options to use with the ps command. You can consult the ps man page to see all the possible parameters that are available. Most Linux administrators have their own set of commonly used parameters that they remember for extracting pertinent information. For example, if you need to see every process running on the system, use the Unix-style –ef parameter combination, like this:

```
```
$ ps -ef
UID  PID  PPID C STIME TTY  TIME CMD
root     1     0  0 09:02 ?  00:00:02 /sbin/init
root     2     0  0 09:02 ?  00:00:00 [kthreadd]
root     3     0  0 09:02 ?  00:00:00 [ksoftirqd/0]
root     4     2  0 09:02 ?  00:00:00 [kworker/0:0]
root     5     2  0 09:02 ?  00:00:00 [kworker/0:0H]
root     6     2  0 09:02 ?  00:00:00 [kworker/u2:0]
root     7     2  0 09:02 ?  00:00:02 [rcu_sched]
root     8     2  0 09:02 ?  00:00:01 [rcuob/0]
root     9     2  0 09:02 ?  00:00:00 [rcuob_bh]
root    10     2  0 09:02 ?  00:00:00 [rcuob/0]
...
$```

```

This format provides some useful information about the processes running:

**UID**: The user responsible for running the process

**PID**: The process ID of the process

**PPID**: The process ID of the parent process (if the process was started by another process)

**C**: The processor utilization over the lifetime of the process

**STIME**: The system time when the process was started

**TTY**: The terminal device from which the process was started

**TIME**: The cumulative CPU time required to run the process

**CMD**: The name of the program that was started in the process

Also notice in the –ef output that some process command names are shown in brackets. That indicates processes that are currently swapped out from physical memory into virtual