A scheduled task is often called a job (just as a process executed in a shell can be called a job). The terms at job and cron job refer to commands or scripts that you have scheduled to be executed at a specific time using the at or cron commands, as described in the sections that follow.

# Automating One-time Tasks

Sometimes you want to perform a task automatically at some future time. For example:

+   - You need to start a backup operation after all employees have left for the evening.
+   - You want to start a large database query during lunch, but you need to leave the office early.
+   - You need to remind several users on the network (and yourself) of a 3:00 meeting.

In each of these cases, you can use the at command to schedule the task for future execution.

# Using the at Command

To automate a task with the at command, you can either enter commands directly at the command line, or you can list them in a file. For complex tasks that require several commands, it's best to list them in a file so you can review them carefully before scheduling them using the at command.

After you create a list of commands to execute in a file, you can schedule execution using this syntax:

```
at -f <filename> <time specification>
```

For example, suppose you created a file called usage_report containing the following lines:

```
logger Starting du to create disk usage report on /home
d u /home > /var/log/du_report
logger Completed disk usage report
```

If you want these commands to execute at 11:30 p.m., you would enter this command:

```
$ at -f usage_report 23:30
```

![](bbox=[0.18, 1.1, 0.26, 1.18])

> When you give a file name to the at command, each of the lines in that file will be executed as if you had entered it at the shell prompt.

The atd daemon will check once per minute for any jobs that have been scheduled using the at command. At 11:30 p.m., the job scheduled by the command above will be executed. Any results from the command (that is, text that would normally be written to the screen) are e-mailed to the user who scheduled the at job. In this example, the commands in usage_report do not generate any screen output—it has been redirected to a file.