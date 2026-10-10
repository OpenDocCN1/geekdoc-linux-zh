# Scheduling Jobs in Linux

To use at to schedule a one-time job for execution at a later time, follow these steps:

+   1. **Run the at command with the date or time when you want your commands executed.**

When you press Enter, the `at>` prompt appears, as follows:
```
at  21:30
at>
```

This method is the simplest way to indicate the time when you want to execute one or more commands — simply specify the time in a 24-hour format. In this case, you want to execute the commands at 9:30 p.m. tonight (or tomorrow, if it’s already past 9:30 p.m.). You can, however, specify the execution time in many different ways. (See Table 1-14 for examples.)

+   2. **At the `at>` prompt, type the commands you want to execute as if typing at the shell prompt. After each command, press Enter and continue with the next command. When you finish entering the commands you want to execute, press Ctrl-D to indicate the end.**

Here is an example showing how to execute the ps command at a future time:
```
at> ps
at> <EOT>
job 1 at 2006-12-28 21:30
```

After you press Ctrl-D, the at command responds with a job number and the date and time when the job will execute.

Table 1-14 Formats for the Time of Execution with the at Command

| Command | When the Job Will Run |
| :--- | :--- |
| at now | Immediately |
| at now + 15 minutes | 15 minutes from the current time |
| at now + 4 hours | 4 hours from the current time |
| at now + 7 days | 7 days from the current time |
| at noon | At noontime today (or tomorrow, if already past noon) |
| at now next hour | Exactly 60 minutes from now |
| at now next day | At the same time tomorrow |
| at 17:00 tomorrow | At 5 p.m. tomorrow |
| at 4:45pm | At 4:45 p.m. today (or tomorrow, if it’s already past 4:45 p.m.) |
| at 3:00 Dec 28, 2006 | At 3:00 a.m. on December 28, 2006 |