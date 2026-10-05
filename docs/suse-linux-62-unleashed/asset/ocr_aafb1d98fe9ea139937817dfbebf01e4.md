# Automating Tasks
CHAPTER 22

```
mv $NEW SOLD
lynx -dump -nolist $URL >$NEW
diff $NEW SOLD
# Wait ten minutes before starting the next comparison.
sleep 60
```

Any changes in the appearance of CNN's home page will appear onscreen session every 10 minutes. This simple approach is less practical than you might first expect because CNN periodically shuffles the content without changing the information. It's an instructive example, however, and a starting point from which you can elaborate your own scripts.

# Conclusions on Shell Programming

Shells are glue; there's a way to get an application to perform an action from the command line, there's almost certainly a way to wrap it in a shell script that gives you power over argument validation, iteration, and input/output redirection. These are powerful techniques and well worth the few minutes of study and practice it takes to begin learning them.

Even small attentions pays off. My personal rule of thumb is to write tiny, disposable, one-line shell scripts when I expect to use a sequence twice during a session. For example, although I have a sophisticated set of reporting commands for analyzing Wide Web server logs, I also find myself going to the trouble of editing a disposable script such as /tmp/r9

```
grep clear ls -t /usr/cern/log/* head -1 grep -v $1 | wc -1
```

to quick, ad hoc queries on recent hit patterns. This particular example reports on the number of requests for pages that include the string clear and exclude the /tmp/r9, in the most recent log. As you become more proficient with shell constructs, it will become easy for you to write one-line shell scripts.

# Scheduling Tasks with cron and Jobs

SuSE Linux comes with several utilities that manage the rubles of job scheduling. It schedules a process for later execution, cron (or crontab—has a couple of interfaces, and different engineers use both these names) periodically launches a process at a certain time of day, day of the week, or even day of the month. Each user can have his own crontab, and output from the executed cron job is sent as an email to the user's mailbox.

![](bbox=[0.875, 0.273, 0.995, 0.423])