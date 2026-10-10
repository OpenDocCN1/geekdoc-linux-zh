# Task 3.8. Schedule Jobs to Run in the Future

The final line of Listing 3.1 specifies the commands that are to be run and the times at which this should occur. This line begins with five fields that specify the time. The fields are, in order, the minute (0–59), the hour (0–23), the day of the month (1–31), the month (1–12), and the day of the week (0–7; both 0 and 7 correspond to Sunday). For the month and day of the week values, you can use the first three letters of the name rather than a number if you like. In Listing 3.1, the command is to run **Monday through Friday** (1–5 in the final time field) on the hour (0 in the first time field) from 8:00 AM through 5:00 PM (8–17 in the second time field). The asterisks in the day of the month and month time fields indicate that the **cron job should run in every month and every day of the month, except when other restrictions exist** (such as in the day of the week field).

The actual command to be run follows the time specification. In this case, it’s the **uptime** command, which is piped through **mail**, which is a simple text-mode mail utility. The **-s** option to **mail** specifies a subject line, and a username follows this.

> Omitting the pipe character (|) and the entire **mail** command would work for this task since **cron** would email the output of the **uptime** command to the user specified by the **MAILTO** variable, but the email with the **uptime** output would lack a **Subject:** header.

You may find that you want to specify the times at which **cron** jobs run in various ways. For instance, you might want to run a **cron** job every other hour or twice a day. You can specify multiple values in several ways:

+   - An asterisk (*) matches all possible values.
+   - A list separated by commas (such as 0,6,12,18) matches any of the specified values.
+   - Two values separated by a dash (–) indicate a range, inclusive of the end points. For instance, **8–17** in the hour field specifies a time of from 8:00 AM to 5:00 PM.
+   - A slash, when used in conjunction with some other multi-value option, specifies stepped values—a range in which some members are skipped. For instance, */10 in the minute field indicates a job that’s run every 10 minutes.

With this information in hand, you should be able to create your own **cron jobs**. You’re not restricted to using system utilities such as **uptime**, either—you can create your own custom scripts to perform complex actions. You can create a single crontab file with multiple **cron** jobs, one per line. Once you type in Listing 3.1 and save it, you can enter it as your user crontab file by passing it to the **crontab** command:

```
$ crontab my-crontab
```

Once it’s installed, you can wait until the hour rolls around to be sure that it’s working as expected—check your email inbox to see if a message with **uptime** output appears.

> For testing purposes, try entering a value in the minute time field that’s just a minute or two in the future. (Change the hour and day-of-week fields, too, if you’re doing this test outside of the range shown in Listing 3.1.) This way you won’t have to wait until the hour ends to see if your **cron job** is working as you expect.