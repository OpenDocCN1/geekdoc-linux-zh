A sample two-line extract from a crontab file looks like this:

```
```
20  1  *  *  *  /usr/bin/calendar -
0   2  *  *  *  /bin/organize_data
```
```

Each line in the crontab file has six columns separated by white space (spaces or tabs). The columns from left to right are:

+   * The minute of the hour (0–59)
* The hour of the day (0–23)
* The day of the month (1–31)
* The month (1–12)
* The day of the week (Sun=0, Mon=1, ... Sat=6)
* The program to be executed at the specified day and time

This rather strange (at first glance) format is necessary to allow you to specify exactly when a process is to run. Without the five different categories for days and time, you can’t precisely specify an event that occurs at random times during a month. As you will see in a moment, these columns are quite easy to complete.

The last column contains the command or script filename that is to be executed. A script that is to be executed can have many lines and call other scripts, or can be only a single line. The first process is initiated when the crontab file matches the day and time. It is important to provide an absolute pathname to the command (even if it’s in your *PATH*), as the cron jobs do not inherit your environment variables and thus don’t know where to look for commands. Also, you must have execute permission for the utility or script. If you are submitting crontab files as a user (not superuser), you must have file permissions or ownership set to allow you normal access, as cron executes the processes as though you owned them.

Each time and day column in the crontab file can contain a single number anywhere in the range of valid numbers, two numbers separated by a minus sign to show an inclusive range (such as 1–5 to show one through five), a list of numbers separated by commas to mean all of the values explicitly specified, or an asterisk meaning all legal values.

Let’s look at the example of a crontab file again to see how this works. In the following example there are three different processes specified:

```
```
20   1  *  *  *  /usr/bin/calendar -
0    2  1  *  0  /bin/organize_data
10,30,50  9-18  *  *  *  /bin/setperms
```
```