To find process about any users we can use pgrep -lu <user> command.

```
root@kemal:-# pgrep -lu root
1 systemd
2 kthread
3 ksoftirqd/0
5 kworker/0:0H
7 rcu_sched
8 rcu_bh
9 migration/0
10 watchdog/0
11 helper
12 kdevtmpfs
13 netns
```

# Kill-Killall

To end process we use kill and killall commands. These commands work as:

+   kill <pid> : to terminate the process with pid number
kill -9 <pid> : fatal hit to the process that we cannot terminate 🙂
killall <process_name> : To terminate all process abot programming/services
kill -9 <process_name> : to kill services process that insists not to be terminated
killall -i <process_name> : To terminate the processes interactively

For example, to terminate all services works with apache, lets use killall apache2 command.