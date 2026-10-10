# Running a Single Future Job

Sometimes cron is overkill. You might simply want to run a single command at a specific point in the future on a one-time basis rather than on an ongoing basis. For this task, Linux provides another command: at. In ordinary use, this command takes a single option: a time. (Options to fine-tune at’s behavior are also available.) The program then prompts you to enter commands that it will execute at the specified time. When you’re done entering commands, press Ctrl+D to terminate input. Alternatively, you can pass a file with commands by using the -f parameter to at, as in at -f commands.txt noon to use the contents of commands.txt as the commands you want to run at noon.

The scenario requires that you email yourself a reminder about a dentist’s appointment. If that appointment is seven days and a few hours in the future, you might do the job like this:

```
```
$ at now + 7 days
warning: commands will be executed using /bin/sh
at> echo "Dentist's appointment at 3:00" | mail -s "Reminder" sally
```
```

This sequence will cause an email message with a subject of “Reminder” and the specified text to be emailed to the sally account in precisely seven days. If specifying the time in precisely this way is inconvenient or impossible, you can use any of several other ways:

+   - **Time of day** You can specify the time of day as *HH:MM*, optionally followed by *AM* or *PM* if you use a 12-hour format. If the specified time has already passed, the operation is scheduled for the next day at that time.
+   - **noon, midnight, or teatime** These three keywords stand for what you’d expect (teatime is 4:00 PM).
+   - **Day specification** To schedule an at job more than 24 hours in advance, you must add a day specification after the time of day specification. This can be done in numeric form, using the formats *MMDDYY*, *MM/DD/YY*, or *DD.MM.YY*. Alternatively, you can specify the date as *month-name day* or *month-name day year*.
+   - **A specified period in the future** You can specify a time using the keyword **now**, a plus sign (+), and a time period, as in **now + 2 hours** to run a job in 2 hours.

The at command has several support tools. The most important of these is atd, the at daemon. This program must be running for at to do its work. Check for its presence using ps. If it’s not running, look for a SysV startup script and ensure that it’s enabled, as described Task 3.7, “Manage Runlevels.”

Other at support programs include atq, which lists pending at jobs; atrm, which removes an at job from the queue; and batch, which works much like at but executes jobs when the system load level drops below 0.8. These utilities are all fairly simple. To use atq, simply type its name. (The program does support a couple of options, but chances are you won’t need them; consult atq’s man page for details.) To use atrm, type the program name and the number of the at job, as returned by atq. For instance, you might type **atrm 12** to remove at job number 12.