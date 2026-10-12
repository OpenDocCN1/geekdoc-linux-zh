```
root 32094 0.0 1.9 2384 1220 ? S 22:03 0:00 httpd
root 32125 0.0 0.6 1148 400 ?/3 S 22:11 0:00 grep http
```

In addition to listing just the parent process, which you can now manipulate as needed, the output also lists the grep command. Because the grep command also listed httpd as one of the components to its search, the command itself was included in the output. Knowing how to locate specific processes by using ps will come in handy later when you look at the possible signals that you can send to each process.

If you replace the aux option with the -ef option, the ps command lists the UID of each process. The output is a full listing of all the current processes, including the UID, PID, and PPID numbers. The following is sample output after running this command on a current system:

```
# ps -ef | more

UID PID PPID C STIME TTY TIME CMD
root 1 0 0 Sep10 ? 00:00:03 init
root 2 1 0 Sep10 ? 00:02:58 [kflushd]
root 3 1 0 Sep10 ? 00:00:30 [kupdated]
root 4 1 0 Sep10 ? 00:00:00 [kpiod]
root 5 1 0 Sep10 ? 00:01:26 [kswapd1]
bin 240 1 0 Sep10 ? 00:00:00 [portmap]
root 287 1 0 Sep10 ? 00:00:02 syslogd -m 0
root 298 1 0 Sep10 ? 00:00:00 [klogd]
daemon 312 1 0 Sep10 ? 00:00:00 /usr/sbin/atd
root 326 1 0 Sep10 ? 00:00:00 crond
root 340 1 0 Sep10 ? 00:00:00 inetd
root 354 1 0 Sep10 ? 00:00:00 [nswapd]
root 368 1 0 Sep10 ? 00:00:01 named
```

Here the UID column shows the username of the process’s owner. The PID field is the process ID, and the PPID column lists the PID of the parent process. The C field shows CPU scheduling information. Though this field is all zeros due to the lack of active processes on our own system, Linux will allot varying amounts of CPU activity to each process based on its importance. Again, the STIME column states the time the process was started, and the TTY field shows the name of the control terminal. In this sample output, the TTY field lists a question mark either because the program is not associated with a specific control terminal or because the process does not require a terminal to start. The latter is the more