Here, *username* is the user for whom you are installing the cron jobs, and *filename* is the file that contains the information about the jobs.

Use the following crontab command to view the cron jobs for a user:

```
```cron
crontab -u username -l
```
```

To remove a user's cron jobs, use the following command:

```
```cron
crontab -u username -r
```
```

![](bbox=[0.14, 0.42, 0.18, 0.51])

> After root creates a user's cron job, users are free to edit it using the command `crontab -e`.

The cron daemon also executes the cron jobs listed in the system-wide cron job file /etc/crontab. Here's the default /etc/crontab file in Red Hat Linux (type cat /etc/crontab to view the file):

```
```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * * root run-parts /etc/cron.weekly
42 4 * * * root run-parts /etc/cron.monthly
```
```

The first four lines set up several environment variables for the jobs listed in this file. The MAILTO environment variable specifies the user who receives the mail message with the output from the cron jobs in this file.

The line that begins with a pound sign (#) is a comment line. The last four lines execute the run-parts shell script (located in the /usr/bin directory) at various times with the name of a specific directory as an argument. Each of the arguments to run-parts—/etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly—are directories. Essentially, run-parts executes all scripts located in the directory that you provide as an argument.

![](bbox=[0.14, 0.0010400000000000001, 0.18, 0.00113])

> The /etc/crontab file has a special format. Between the last time field and the command field you can place a user name. The cron daemon will run the commands or script using that user name.

Table 25-3 lists what those directories contain.