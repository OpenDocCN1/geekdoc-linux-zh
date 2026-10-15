```
at [-f file] -t [[CC]YY]MMDDhhmm[.SS]
at -r job [job ...]
at -l [-q queuename]
at -l [job ...]
atq [-q x] [-v]
atrm job [job ...]
batch [-f file] [-m]
```

For example, to run a script called `fixperms` tomorrow at 3 a.m., you can use the command

```
at 3am tomorrow fixperms
```

The man page has more information about this slick command.

# cron

The other possibility, and the scheduling program that’s used quite a bit more often on Unix systems, is `cron`, known also as `crontab` for the name of the file it executes. Every 60 seconds on your Unix system, the OS has the `cron` daemon check to see if any new commands need to be invoked.

Unfortunately, writing `crontab` entries can be a wee bit tricky, but here’s a prototypical entry in a user’s `crontab`, added by invoking the command `crontab -e`:

Click here to view code image

```
51 7 * * 1-5 $TRIVIAHOME/mailit -h -i -a
```

The fields in a `crontab` entry are, in order, minute, hour, day of month, month, day of week, command with optional flags or parameters. Asterisks in fields indicate that all possible values of that field are matched, so this `crontab` entry should be read as “at 7:15 a.m. on Monday through Friday (1-5 in field 5) of any day of the month or month of the year, run the `mailit` program with the -h, -i, and -a flags.”

After having worked with Unix for many years, I find the `crontab` facility invaluable and typically have dozens of different scripts, programs, and utilities scheduled to run at different times of the day, week, month, or year. Heck, you can even use it for critical birthday reminders if you need to!

# Tip

Mac systems and all Linux systems also have `cron`, which means you can easily have recurring programs or scripts on those systems, too.

Learn more at `man crontab`.