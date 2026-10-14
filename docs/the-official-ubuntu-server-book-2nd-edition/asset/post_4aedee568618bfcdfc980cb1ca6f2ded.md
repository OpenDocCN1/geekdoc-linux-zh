
## Cron

Most of the time, you will find that instead of using at, you will want to run commands periodically. For that you will use cron. Cron is a daemon that runs in the background on your Linux system. Each user and the system itself has a cron table (called crontab) that lists what jobs they would like run as well as how frequently they should be run.

The systemwide crontab is located at /etc/crontab and is a good place to look to get an idea of cron's syntax:

```
$ cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab, you don't have to run the 'crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user    command

17 * * * * root    cd / && run-parts --report /etc/cron.hourly

25 6 * * * root    test -x /usr/sbin/anacron ||
( cd / && run-parts --report /etc/cron.daily )

47 6 * * 7 root    test -x /usr/sbin/anacron ||
( cd / && run-parts --report /etc/cron.weekly )

52 6 1 * * root    test -x /usr/sbin/anacron ||
( cd / && run-parts --report /etc/cron.monthly )
#
```

Each crontab entry in this file starts with a few fields that tell cron when that entry should be run. Then the entry states which user will execute the command (root in these examples), and finally it lists the command to run. Let's look at a few of these lines to see how the syntax works:

```
25 6 * * * root    test -x /usr/sbin/anacron ||
( cd / && run-parts --report /etc/cron.daily )
```

The first field in this line tells cron what minute on the hour to trigger the command, and the second field sets which hour. In this example the command will be triggered at 6:25 AM. The next three fields allow you to set the day of the month, the month, or the day of the week to run the command. In our case we have * in each of those fields, which acts like a wildcard so that cron will run the command at 6:25 AM every day.

The next line in the crontab shows you how to have a command run once a week:

```
47 6 * * 7   root   test -x /usr/sbin/anacron ||
    ( cd / && run-parts --report /etc/cron.weekly )
```

In this command the minute field is set to 47, the hour field is set to 6 (so 6:47 AM), the day of month and month fields are wildcards, and the day of week field is set to 7. The day of week field can accept a number between 0 and 7 with either 0 or 7 representing Sunday, 1 representing Monday, 2 Tuesday, and so on. In this case the command will be run every Sunday at 6:47 AM.

The final line in the file shows you how to have cron execute a command once per month:

```
52 6 1 * *   root   test -x /usr/sbin/anacron ||
    ( cd / && run-parts --report /etc/cron.monthly )
```

Here we see that the minute field is set to 52, the hour field is set to 6, and the day of month field is set to 1, while the rest of the fields are wildcards. This tells cron to run that command on the first day of the month at 6:52 AM. If I wanted the command to run on the 20th day of the month, I would change the 1 to a 20.

In addition to the standard numbers you can put in each field, cron accepts ranges and multiple numbers separated by commas. You can define a range by putting a dash between two numbers. For instance, if I wanted to run a command every 15 minutes, my fields would look like

```
0,15,30,45 * * * *    root    mycommand
```

This way cron will run the command at 0, 15, 30, and 45 minutes after the hour. If I wanted to run a command at 9 AM only on Monday through Friday I could say

```
0 9 * * 1-5    root    mycommand
```

Finally, cron also accepts fractions, which saves you from having to type in all of the comma-separated numbers. For instance, a shorthand form of the above command that runs every 15 minutes could be

```
*/15 * * * *    root    mycommand
```

While in the past many administrators would put their commands directly into the /etc/crontab file, over time that caused the file to get quite large and difficult to manage. Realistically, you usually want to run a command either every hour, every day, every week, or every month. Instead of putting those commands directly into /etc/crontab, all you have to do is create a file that has the shell script you want to run and then place it in either /etc/cron.hourly/, /etc/cron.daily/, /etc/cron.weekly/, or /etc/cron.monthly/, and cron will run it at that frequency. If you look in those directories, you’ll find that a number of other services on your system already have scripts set up there that you can emulate.

Even if you do have a command you want to run that doesn’t conveniently fit into one of the above directories, you still don’t want to add it directly to /etc/crontab. Instead, Ubuntu has set up an /etc/cron.d/ directory. To use this directory, create your custom /etc/cron.d-style file that follows the proper syntax, and then place it in this directory. For instance, if I wanted to run my special backup script located at /usr/local/sbin/mybackup at 7 AM every day, I could create a file named /etc/cron.d/mybackup that would contain the following:

```
# /etc/cron.d/mybackup: run my backup script outside of
# regular cron.daily

SHELL=/bin/sh

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

0 7    * * *    root  /usr/local/sbin/mybackup
```
