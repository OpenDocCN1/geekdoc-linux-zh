For security purposes, there are filters available to limit who can edit the *cron* configuration (\textit{crontab}) files. Users in the /etc/cron.allow file are the \textit{only} users able to edit their files. If that file is empty, the system looks for users in the /etc/cron.deny file, which lists users barred from editing *cron* files. The root user isn't affected by either.

# ## crontab Command Syntax

The schedule consists of a series of files called \textit{crontabs} (cron table) that tells *cron* what to run and when to run it. Crontab files for users are stored in /var/spool/cron, with the crontab name matching the username. The administrators files are kept in /etc/crontab, and there is an /etc/cron.d directory that programs can use to store their own schedule files.

The crontab schedule files are edited using \textit{crontab} -e. They use a special format to specify the when to run. Each line has either six or seven fields, and specifies one command. The first five fields on each line tell which minute, hour, day, month, and weekday to run a command. The next spot on a line is an option for administrators and tells whose user rights to run the command under, and last is the command itself. Valid options for the schedule fields are a *, which matches anything, a number, which matches that exact value, two numbers with a dash between them for a range of values, or a list of values separated by commas to match each single value. The command can be anything that works. Altogether, it looks like this:

```
crontab -e
30 17 * * 1-5 do\_something.sh
```

That means 30 min after the hour of 5:00 PM. every day of the month, every month of the year (that is, Monday through Friday).

*crontab* uses the text editor that your profile is set to use; chances are you'll be using your old friend \textit{vi}. Remember to press \textless Ctrl \textgreater d, \textless Esc \textgreater to get back to ex mode, then :wq to save and exit. See vi section if you need a refresher.

You can also use \textit{crontab} -l to display the contents of your crontab file, and \textit{crontab} -r to delete it.

# ## atq

If you just want to have something run a bit later rather than schedule it to keep reoccuring, you can use the \textit{at} command. It accepts commands from either a file (use -f) or standard input, ending with a \textless Ctrl \textgreater d. A single ctrl-d is sufficient if there is nothing else on the line. It takes two ctrl-ds if there is more text on the line. For example, at \textless ls -l \textgreater text.txt