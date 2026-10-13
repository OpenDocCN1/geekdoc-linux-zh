# EXERCISE 9-1

# Create a cron Job

In this exercise, you will modify the basic Red Hat cron job settings to read a text file at 1:05 P.M. every Monday in the month of January. To do so, you'll need to create a directory for yearly cron jobs. To do this, use the following steps:

+   1. Log in as a regular user.
+   2. Create a /etc/cron.yearly directory. Add a file called taxrem, which reads a text file from your home directory. A command such as the following in the taxrem file should suffice:
+   3. Open up the crontab for your account with the crontab -e command.
+   4. Add an appropriate command to the crontab. Based on the conditions described, it would read as follows:
+   5. Don’t forget directives such as SHELL=/bin/bash at the start of the script.
+   6. Save and exit. Confirm the existence of the user cron file in the /var/spool/cron directory. That file should have the same name as the user.

```
cat ~/reminder
```

Make sure to add appropriate lines to the reminder file in your home directory, such as "Don’t forget to do your taxes!" Make sure the taxrem file is executable with the chmod +x /etc/cron.yearly/taxrem command.

```
5 13 * 1 1 root run-parts /etc/cron.yearly
```

# Running a Job with the at System

Like cron, the at daemon supports job processing. However, you can set an at job to be run once. Jobs in the cron system must be set to run on a regular basis. The at daemon works in a way similar to the print process; jobs are spooled in the /var/spool/at directory and run at the specified time.

You can use the at daemon to run the command or script of your choice. For the purpose of this section, assume that user michael has created a script named 797 in his home directory to process some airplane sales database to another file in the same directory called sales.