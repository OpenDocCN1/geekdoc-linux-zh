# 28.3.3 Listing Your CRON Jobs

To list all of the CRON jobs you have scheduled, use crontab with the -l option.

⇒ To list your CRON jobs, type:

```
$ crontab -l [RET]
```

# 28.4 Watching a Command from Time to Time

Use watch to observe the output of a command and watch it run from time to time. It runs the command you give as an argument, repeatedly, every two seconds, until it is interrupted. Each time the command is run, the display is updated with the new results. This is particularly useful for when you want to closely watch some files in a directory and note the changes as they occur.

⇒ To watch the detailed contents of the current directory, type:

```
$ watch ls -l [RET]
```

This command will display the contents of the current directory in the terminal you run it in, and it will continually update every two seconds. To change the interval, give it as an argument to the -n option.

⇒ To watch the detailed contents of the current directory, updating by the second, type:

```
$ watch -n 1 ls -l [RET]
```

Use the -d flag to highlight the differences in the updates.

⇒ To watch the detailed contents of the current directory, updating every ten seconds, and highlighting all the differences, type:

```
$ watch -d -n 10 ls -l [RET]
```

NOTES: Sometimes you might find it nice to run your watch session in a little xterm of its own. If you're not in X, you might want to devote a console terminal to it.