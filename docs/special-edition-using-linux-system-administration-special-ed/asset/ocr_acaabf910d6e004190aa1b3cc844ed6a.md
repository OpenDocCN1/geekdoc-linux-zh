+   - Multiple values can be separated by commas. For instance, to schedule a task on the 1st and the 15th day of the month, use `1,15` in the day field.
+   - Ranges of numbers of the form `a-b` can be used. For instance, to schedule a task to run at 4:00 p.m., 5:00 p.m., and 6:00 p.m., you could use `16-18` in the hour field.
+   - Ranges of numbers can be stepped through in increments using the form `a-b/c` where `a-b` is the range and `c` is the increment. For instance, to schedule a task to run every other hour between 10:00 a.m. and 10:00 p.m. you could use `10-22/2` in the hour field.
+   - An asterisk can be used to indicate the entire range of possible values in a field. For instance, to schedule a task to run every day of the month, put an asterisk in the day field.

Consider the following examples of the time and date fields from `crontab` entries:

+   - `0 4 * * *`: A job scheduled to run every day at 4:00 a.m.
+   - `30 4 * * 1`: A job scheduled to run every Monday at 4:30 a.m.
+   - `0 2,4,6 * * 1`: A job scheduled to run every Monday at 2:00 a.m., 4:00 a.m., and 6:00 a.m.
+   - `0 16 2 * *`: A job scheduled to run at 4:00 p.m. on the second day of every month.
+   - `30 16 * 3 thu`: A job scheduled to run at 4:30 p.m. on every Thursday in March.
+   - `0 12 4 jun *`: A job scheduled to run at noon on the June 4th of every year.

The command field bears some special attention. In particular, it is worth noting that commands scheduled to run are run by crontab by passing them through the `/bin/sh` shell.

However, the non-interactive nature of commands run through crontab is problematic when an application expects interactive input through the standard input. You can pass data to a command through the standard input by using percent signs. The first percent sign following the command marks the start of data considered to be standard input, and each subsequent percent sign serves as a new line character in the standard input to the command when it runs. For instance, consider the following command in the command field:

```
0 8 * * 5 /bin/mail -s ''Friday!'' user@some.host%It's Friday%Thank God%Me.
```

This command will send the email message:

```
It's Friday

Thank God

Me.
```

to user@some.host each Friday afternoon at 8:00 a.m.