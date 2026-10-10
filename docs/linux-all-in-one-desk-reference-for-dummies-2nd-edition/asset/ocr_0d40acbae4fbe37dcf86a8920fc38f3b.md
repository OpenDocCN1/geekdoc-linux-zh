# 412 Scheduling Jobs in Linux

```
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The first four lines set up several environment variables for the jobs listed in this file. The MAILTO environment variable specifies the user who receives the mail message with the output from the cron jobs in this file.

The line that begins with a # is a comment line. The four lines following the run-parts comment execute the run-parts shell script (located in the /usr/bin directory) at various times with the name of a specific directory as argument. Each of the arguments to run-parts — /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly — are directories. Essentially, run-parts executes all scripts located in the directory that you provide as an argument.

Table 1-16 lists the directories where you can find these scripts and when they execute. You have to look at the scripts in these directories to know what executes at these periodic intervals.

Table 1-16 Script Directories for cron Jobs

| Directory Name | Contents |
| --- | --- |
| /etc/cron.hourly | Scripts execute every hour |
| /etc/cron.daily | Scripts execute each day |
| /etc/cron.weekly | Scripts execute weekly |
| /etc/cron.monthly | Scripts execute once each month |