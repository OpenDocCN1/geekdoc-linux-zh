For example, to output both U.S. holidays and famous births and deaths when you run `calendar`, your calendar file would include the two lines given in Figure 27-4.

**NOTES:** You can, of course, share your own calendar files with other users; this is useful for making special calendars for a group or organization. If the calendar file is in the current directory or `/usr/share/calendar`, you can just give the file name; otherwise, give its full path name in the `include` statement.

# 27.4.3 Automatic Appointment Delivery

You can automate your appointment service so that your appointments and reminders are delivered each time you log in or start a new shell, or you can have the day’s reminders emailed to you each morning.

Add `calendar` to your `.bashrc` file to output the day’s appointments and reminders every time you log in or start a new shell (see Recipe 3.7.3 [Using Shell Startup Files], page 86).

If you keep your calendar file in a directory other than your home directory, make sure that `calendar` (the tool) is called from that directory. For example, if your calendar file is in your `/doc/etc` directory, you’d put the following line in your `.bashrc` file:

```
cd "/doc/etc; calendar; cd
```

To have the system send you the day’s appointments in email, use `crontab` to schedule a daily CRON job that runs `calendar` and, if there is any output, mails it to you with `mail` (see Recipe 28.3 [Scheduling Commands], page 557).

To do this, add the following line to your `crontab` file (if you don’t have one, just put this line in a text file called `crontab` somewhere in your home directory tree):

```
45 05 * * 1-5 calendar | mail -s 'Your Appointments' joe@example.org
```

The “45 05 * * 1-5” specifies that these commands be run at 5:45 a.m. on every weekday. The rest of the line is the series of actual commands that are run: The `calendar` tool is run on your personal calendar file, and if there is any output, it’s mailed to joe@example.org (replace that with your actual email address, or with your username on your local system if you check mail there).

Add this new entry to the schedule by running the `crontab` tool with the name of your `crontab` file as an argument.