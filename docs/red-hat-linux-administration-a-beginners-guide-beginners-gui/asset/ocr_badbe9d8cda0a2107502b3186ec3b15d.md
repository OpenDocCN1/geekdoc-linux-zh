# 8.6 Using the cron Program

The **cron** program allows any user in the system to schedule a program to run on any date, at any time, or on a particular day of week, down to the minute. Using **cron** is an extremely efficient way to automate your system, generate reports on a regular basis, and perform other periodic chores. (Not-so-honest uses of **cron** include having it invoke a system to have you paged when you want to get out of a meeting!)

Like the other services you've considered in this module, **cron** is started by the boot scripts and is most likely already configured for you. A quick check of the process listing should show it quietly running in the background:

```
```bash
[root@tedford /root]# ps auxx | grep cron | grep -v grep
root    341   0.0   0.0   1284   112 ?   S   Jun21   0:00 crond
[root@tedford /root]#```
```

The **cron** service works by waking up once a minute and checking each user's **crontab** file. This file contains the user's list of events that they want executed at a particular date and time. Any events that match the current date and time are executed.

The **crond** command itself requires no command-line parameters or special signals to indicate a change in status.

# The crontab File

The tool that allows you to edit entries to be executed by **crond** is **crontab**. Essentially, all it does is verify your permission to modify your **cron** settings and then invoke a text editor so that you can make your changes. Once you're done, **crontab** places the file in the right location and brings you back to a prompt.

Whether or not you have appropriate permission is determined by **crontab** by checking the */etc/cron.allow* and */etc/cron.deny* files. Neither of these files exists by default in Red Hat Linux 8.0, and therefore they are not consulted. However, if either of these files exists, a user must be explicitly listed there for their actions to be effected. For example, if the */etc/cron.allow* file exists, your username must be listed in that file in order for you to be able to edit your **cron** entries. On the other hand, if the only file that exists is */etc/cron.deny*, unless your username is listed there, you are implicitly allowed to edit your **cron** settings.

The file listing your **cronjobs** (often referred to as the **crontab** file) is formatted as follows. All values must be listed as integers.

![](bbox=[0.15, 0.92, 0.6, 0.94])