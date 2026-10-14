+   4. Send the PID of your bash shell as SIGCONT. What happened and why?
+   5. Send the PID of your bash shell as SIGKILL. What happened and why?

# Process Priorities

Log in to tty1 as the root user and perform the following actions in order. For each action, write down the command(s) that you used. When finished, log out of tty1.

+   1. Start the ps -1 command with the default nice value. What nice value is shown in the output?
+   2. Start the ps -1 command with a nice value of -20 and verify the correct nice value in the output. Did this command run with high or low priority? Which users can run this command?
+   3. Start the ps -1 command with a nice value of +19 and verify the correct nice value in the output. Did this command run with high or low priority? Which users can run this command?

# Scheduling Processes Using the at Daemon

The at command is versatile in that it can understand nearly any time format. Log in to tty1 as the root user, ensure that the at daemon is running, and schedule the date and who commands to run at a time (use the at teatime command). When you have finished scheduling the at job, note the time that the two commands will be scheduled. Following this, remove your at job and use the manual or info pages to research other time formats that can be used with the at command. When finished, log out of tty1.

# Cron Tables

Write the lines that you could use in your crontab to schedule the /bin/sample command to run:

+   1. every Friday at 1:30 a.m.
+   2. at 4:30 p.m. on May 15th only
+   3. at 4:00 p.m. and 4:30 p.m. on the first Sunday of every month
+   4. every 10 minutes from 9:00 a.m. to 5:00 p.m. on Monday
+   5. at 8:15 a.m. and 6:30 p.m. Monday to Friday