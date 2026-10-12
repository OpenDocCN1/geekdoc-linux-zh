
## Examples of Using cron

Now you'll take a look at some sample crontab file entries and figure out exactly what each one is doing.

The following crontab command will cause the string "It is 1 am" to be outputted everyday at 1:00 a.m. This will result in the owner of the crontab file receiving an email every day at 1:00 a.m. with the words "It is 1 am" in the email body.

```
0 1 * * * echo "It is 1 am"
```

The following is a slightly more complex example:

```
1 5 10 jul * echo 'It is July 10th'
```

This crontab command is similar to the first example, but this time the string outputted reads "It is July 10th" instead of "It is 1 am". In addition, this time the command is executed only once a year on July 10th at 5:01 in the morning.

Take a look at an example that uses a list value:

```
* 2,5,15 4,20 * * find / -name core -print
```

This example will send you an email with a list of every core file on your system and will be executed at 2:00, 5:00, and 15:00 on the 4th and 20th days of each month. Here the list values allow you to specify more than one value for a single field.

The following is an example using range values with a cron command:

```
* 5 4-10 0-3 * find / -name core -print
```

This example does the same things as the last example, but this time it is executed at 5:00 on the 4th, 5th, 6th, 7th, 8th, 9th, and 10th days of the months of January, February, March, and April. Range values are very useful when you want to match a span of values.

The following is another example, making use of the step value notation:

```
* */2 * * sat rm -rf /tmp/*
```

In this case, the command rm -rf /tmp/* is executed every other hour on every Saturday. The value */2 is true every second hour of the day and is equivalent to using the list 0,2,4,6,8,10,12,14,16,18,20,22.

We have covered all the standard features and usage of the cron utility. You should have a solid understanding of how to use cron and be able to implement automated jobs using cron. The next section takes a look at the process of debugging cron jobs and covers a few techniques for ensuring that all cron jobs run as expected.

## Debugging cron Jobs

There are a number of techniques you can use to debug your cron jobs. If you are not careful, your cron jobs can have unintentional results, such as deleting files unexpectedly. This could happen if you search for *.tmp, not realizing that a music composition program uses .tmp extensions for timpani files. Because of this, it is very useful to learn a few tips and tricks for debugging cron jobs. This section explores exactly that, covering the following topics:

- Capturing output
- Using printf and echo as debugging tools
- Examining the log files

### Capturing Output

You can redirect the output of cron jobs to specific files using the standard output redirection syntax. This is very useful because it will create files after each cron job is run that you can examine for errors and debug if necessary. The following is an example of a crontab command that will output all errors from the specified command to a file:

```
0 1 * * * rm -rf /tmp/* 2>/home/dbarber/del_tmp.cron
```

Using this command, if any errors occur when cron is trying to execute the rm -rf /tmp/* command, they will be put into the /home/dbarber/del_tmp.cron file. Every time the cron job runs, it overwrites the contents of the /home/dbarber/del_tmp.cron file with the errors from the latest cron job.

Redirecting the output of a command can also be very useful because it will cause all output from that command to go to a file, instead of having an email sent to you. If you find that you are getting a number of useless emails from a specific cron job, you may want to change the crontab entry for that job, redirecting the output to a file.

### Using printf and echo as Debugging Tools

You can use both the printf and echo commands in your crontab files to print out exactly what the commands in your crontab entry are doing. When printf or echo displays any output, that output will be mailed to the user of the crontab file so that he or she can examine exactly what his or her cron job is doing.

For example, say you have the following shell script that you want to execute every day at a specific time:

```
#!/bin/sh
rm -rf /home/dbarber/backup/*
cp -r /home/dbarber/files/* /home/dbarber/backup/
```

If something goes wrong with this script, you will be emailed any error messages that are outputted from the commands in the script. However, if you have a number of these types of scripts running daily, the error messages by themselves may actually be confusing, and you may not know exactly what command is causing the error. It is a very good idea to print out each command before you execute it so that when the output is emailed to you, you will have a listing of each command executed. If any errors occur, they will appear directly after the command. You will immediately be able to figure out what command caused the error.

The following is the same script, this time with some echo commands outputting some extra information:

```
#!/bin/sh
echo Backing up files in /home/dbarber/files to /home/dbarber/backup
echo rm -rf /home/dbarber/backup/*
rm -rf /home/dbarber/backup/*
echo cp -r /home/dbarber/files/* /home/dbarber/backup/
cp -r /home/dbarber/files/* /home/dbarber/backup/
echo end of backup script
```

To get cron to execute that script once a day at 2:00 a.m., add the following file to your crontab file (assuming you saved the previous script as backup.sh):

```
0 2 * * * /home/dbarber/backup.sh
```

When adding lots of output to your cron scripts, be careful to use caution if the cron script executes several times each day, because it will be sending you an email each time that script executes. If each email has a number of lines of output, you will find that your disk space may start to disappear if you do not delete the emails regularly. This is especially true for scripts run as root, because you may not log in as root for several days and the amount of email sent from cron can grow quite rapidly.

Of course, you can also use the printf command instead of echo if you want to specifically format the output. This might be needed if the files are imported into a database of spreadsheet. For many situations however, the echo command is more than sufficient.

### Examining the Log Files

There are several files that are under the /var/log directory where cron logs all of commands it runs. The files are called cron, cron.1, cron.2, cron.3, and cron.4, and you must have superuser privileges to view their contents. The following is a listing of the contents of the /var/log/cron file:

```
# cat /var/log/cron
root (08/15-04:22:00-3862) CMD (run-parts /etc/cron.weekly)
root (08/15-05:01:00-3974) CMD (run-parts /etc/cron.hourly)
root (08/15-06:01:00-4003) CMD (run-parts /etc/cron.hourly)
root (08/15-07:01:00-4015) CMD (run-parts /etc/cron.hourly)
root (08/15-08:01:00-4041) CMD (run-parts /etc/cron.hourly)
root (08/15-09:01:00-4069) CMD (run-parts /etc/cron.hourly)
root (08/15-10:01:00-4122) CMD (run-parts /etc/cron.hourly)
root (08/15-11:01:00-4154) CMD (run-parts /etc/cron.hourly)
root (08/15-12:01:00-4338) CMD (run-parts /etc/cron.hourly)
root (08/15-13:01:00-4677) CMD (run-parts /etc/cron.hourly)
root (08/15-14:01:00-4977) CMD (run-parts /etc/cron.hourly)
root (08/15-15:01:00-4957) CMD (run-parts /etc/cron.hourly)
root (08/15-16:01:00-4997) CMD (run-parts /etc/cron.hourly)
root (08/15-17:01:00-5118) CMD (run-parts /etc/cron.hourly)
```

In the /var/log/cron file, you have all the times that cron has been run in the past day. As you can see, the contents of the /etc/cron.weekly directory was executed at 4:22 a.m., and the contents of the /etc/cron.hourly directory was executed every hour on the first minute of the hour.

The files cron.1, cron.2, and cron.3 contain similar information, although slightly older than cron. The cron log files are great to check on whether your cron jobs are executing at the correct time or whether they are even executing at all. If you have many cron jobs set up on your system, it is wise to check the cron log files every few days just to make sure that all the cron jobs are executing properly.

## Summary

This chapter examined job automation in detail, specifically covering the reason for automating jobs as well as exactly how to go about scheduling jobs to be automated. You should have a solid understanding of the concept of job automation and how to employ it in your system administration duties.
