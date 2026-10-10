Disallowed users list  The /etc/cron.deny file contains a list of users who should be denied access to cron. If this file is present, any user whose name appears in the file is denied access to cron, but all others may use it, assuming executable permissions and the allowed users list don't restrict access.

Exercise 7.2 guides you through the process of creating user cron jobs.

# EXERCISE 7.2

# Creating User *cron* Jobs

cron jobs can be a useful way to run programs at regular times. In this exercise, you’ll create a simple user cron job that will mail you the output of an `ifconf`g command on a daily basis. This exercise assumes that you’re authorized to use cron as an ordinary user. To configure your cron job, follow these steps:

+   1. Log into the Linux system as a normal user.

+   2. Launch an xterm from the desktop environment’s menu system, if you used a GUI login method.

+   3. Create and edit a file called *cronjob* in your home directory. Use your favorite text editor for this purpose. The file should contain the following lines:

```
SHELL=/bin/bash
MAILTO=*yourusername*
00 12 * * * /sbin/ifconf`g
```

Be sure to type these lines exactly; a typo will cause problems. One exception: Substitute your e-mail address on the Linux system or elsewhere for *yourusername*; cron uses the MAILTO environment variable to determine to whom to e-mail the output of cron jobs.

+   4. Type `crontab cronjob` to install the *cronjob* file as a cron job. Note that this command replaces any existing user cron jobs that may exist. If you’ve already defined user cron jobs for your account, you should edit your existing *cronjob* file to add the line calling `ifconf`g rather than create a new file.

+   5. Wait for 12:00 noon (00 12 in the cron time format). When this time rolls around, you should have a new e-mail waiting for you with the contents of the `ifconf`g output.

Instead of waiting for 12:00 noon, you can substitute a time that’s a couple of minutes in the future. Remember that cron specifies minutes first, followed by the hour in a 24-hour format. For instance, if you create the file at 3:52 p.m., you might enter `54 15` as the first two numbers on the final line of the file; this will cause the cron job to execute at 15:54 on a 24-hour clock, or 3:54 p.m.