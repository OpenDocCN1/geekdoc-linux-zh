# 10.4.1 Executing commands at a later time (at)

The at command can be used to execute a command once at a specified time, for example, if you want to execute a program such as a complex database elaboration at a time when the computer is not too loaded. You could also use the batch command, which is particularly suitable for this purpose, because it executes the specified commands only if the system has sunk below a specified level. The example in Listing 10.29 shows how to delete the file /etc/nologin.tty1 at 20:00.

The exact time of the at command depends on how frequently the atrun command is executed. On my system, for example, this command is only called every five minutes (see Section 10.4.3).

The at command expects the commands to be executed from the standard input. After entering the command, Ctrl+D must be pressed as end mark. This inserts the task into the job queue. To verify whether the at command has correctly stored the command, you can list the queue by means of the atq command (see Listing 10.30).

Date and time specify when the task is to be executed, and the owner of the task and an ID number are listed as well. If a job is to be cancelled, it can be removed from the job queue by means of the atm command (see Listing 10.31).

```
(Linux):# at 20:00
> rm -f /etc/nologin.tty1
> Ctrl-D
Job c00c95ff4.0 will be executed using /bin/sh
```

Listing 10.29 Starting a program with at.

| Date | Owner | Queue | Job# |
|---|---|---|---||
| 20:00:00 | 02/03/95 | root | c | c00c95ff4.00 |

Listing 10.30 Output of the atq command.

```
(Linux):# atm c00c95ff4.00
```

Listing 10.31 Removing an at job with atm.

The at command accepts time specifications in different formats. The time of day can be indicated as HH:MM or HHMM. Other legal values are midnight, noon, and teatime (16:00).