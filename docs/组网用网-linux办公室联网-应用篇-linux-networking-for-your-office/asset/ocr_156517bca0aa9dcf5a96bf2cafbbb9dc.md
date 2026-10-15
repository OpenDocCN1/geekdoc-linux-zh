# CAUTION

Before you install any scripts or commands for execution by cron, you should be positive that the scripts or commands do what you expect them to do. In the case of a script, run it manually, and check how it handles errors. For instance, if a remote machine has been turned off, what does the script do? Does it notify you—say by email—of the error, or does it simply back up an empty directory with no indication that there's a problem? Above all else, you don't want a script that will cause the server's disk to fill, or that will cause CPU use to shoot off the scale to run when you're not around to quickly fix the problem.

Your needs may be more specific than a once-a-week backup, of course. In that case, you need to create a custom cron job. You can do this by typing

```
crontab -u root -e
```

The specifics of this example assume that you're running crontab as root and that you want to create a cron job to run as root (you can also create a personal non-root cron job in the same way). The -e parameter to crontab opens an editor in which you can create a crontab file (note the dual use of the word crontab—in reference to both a file and a command). If you prefer, you can create the crontab file in whatever editor you prefer and use the crontab command to install it in the system.

Lines in a crontab file are either environment variable settings or cron commands.

Environment variable settings take the form

```
VARIABLE = value
```

You might want to set some common variables in this way, such as:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
```

cron commands take the form

```
minute hour day-of-month month day-of-week command
```

The first five fields specify the time, and the rest of the line is the command to be run. In the case of complex commands, you should probably create a shell script and specify the complete path to the script. The various time fields take values as follows:

+   minute—Values 0–59.
+   hour—Values 0–23.
+   day-of-month—Values 0–31.