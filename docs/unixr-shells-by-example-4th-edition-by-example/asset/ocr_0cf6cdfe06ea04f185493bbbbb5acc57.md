can be in military or 12-hour AM/PM format. Time can also be specified as a relative to the current time with a + sign. With a − sign, the event is removed from the list.

# FORMAT

```
sched
sched [-+]hh:mm command
sched -n
```

# EXAMPLE

```
1    > sched 14:30 echo '^G Time to start your lecture!'
2    > sched 5PM  echo Time to go home.
3    > sched +1:30 /home/ellie/scripts/logfile.sc
4    > sched
     1    17:47 /home/scripts/logfile.sc
     2    5PM   echo Time to go home.
     3    14:30 echo '^G Time to start your lecture!'
5    > sched -2
     > sched
     1    17:47 /home/scripts/logfile.sc
     2    14:30 echo '^G Time to start your lecture!'
```

# EXPLANATION

+   1. The sched command schedules the echo command to be executed at 14:30. At that time a beep will sound (Ctrl-G) and the message will be displayed.
+   2. The sched command will schedule the echo command to be executed at 5 PM.
+   3. The script, logfile.sc, is scheduled to be executed 1 hour and 30 minutes from now.
+   4. The sched command displays the scheduled events, in numeric order, the last one first.
+   5. With a numeric argument, sched will remove the numbered job from the scheduled list. Job number 2 was removed, as shown in the output of sched.

a. To get the ^G into the echo statement, type Ctrl-M, followed by Ctrl-V, followed by Ctrl-G.

> 8. From the tcsh man page: “A command in the scheduled-event list is executed just before the first prompt is printed after the time when the command is scheduled. It is possible to miss the exact time when the command is to be run, but an overdue command will execute at the next prompt.”