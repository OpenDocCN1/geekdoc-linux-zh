To use crontab to submit your own cron jobs, you create a file that has a time specification and a command to execute. Unlike the at command, you must create a file containing this information; you cannot enter cron job commands interactively. Suppose, for example, that you wanted to run the du command on /home and sort the results every morning at 1:00 a.m. You do this by following these steps:

+   1. Create a text file containing the time specification and the command you want to execute. For this example, the file contains the following line (you need to submit this cron job as root so that the du command can access all home directories):
+   
+       0 1 * * * du /home | sort > /root/disk_usage
+   2. Submit the file to the crond daemon using the crontab command. If the file you created in Step 1 were called du_nightly, the command would look like this:
+   
+       # crontab du_nightly

Notice that the command shown in Step 1 fits on a single line.

If you need to perform more complex tasks, you can create two files: a shell script and a cron job specification. You cannot use multiple command lines within a single cron job specification.

Suppose, for example, that you had developed a series of shell scripts that check the security of the Linux system by reviewing log files, checking network activity, and watching user login activity. If the script that performed all of these activities were called secure_system, you could run that script every morning at 1:30 a.m. by adding this line to your du_nightly file before submitting the file using the crontab command:

```
30 1 * * * /sbin/secure_system
```

The full path name of the script is included so that the crond daemon is able to locate the script when it attempts to execute this job.

In the /etc/crontab file shown previously, you saw environment variables at the beginning of the file. You can also include environment variables in crontab specification files that you create. For example, suppose you want the du_nightly cron job to be executed via the root user account so that it can access all home directories, but you want an e-mail message sent to your regular user account so you won't have to log in as root to read the message. To do this, you can include a MAILTO variable at the top of the du_nightly file. The du_nightly file now looks like this:

```
MAILTO=ewells
0 1 * * * du /home | sort > /root/disk_usage
30 1 * * * /sbin/secure_system
```