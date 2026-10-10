Step values can be used in conjunction with ranges. Following a range with “`/number`” specifies skips of the number’s value through the range. For example, “`0-23/2`” can be used in the hours field to specify command execution every other hour. (The alternative in the V7 standard is “`0,2,4,6,8,10,12,14,16,18,20,22`”.) Steps are also permitted after an asterisk, so if you want to say “every two hours”, just use “`*/2`”.

Names can also be used for the “month” and “day of week” fields. Use the first three letters of the particular day or month (case doesn’t matter). Ranges or lists of names are not allowed.

The “sixth” field (the rest of the line) specifies the command to be run. The entire command portion of the line, up to a new line or % character, will be executed by /bin/sh or by the shell specified in the SHELL variable of the crontile. Percent-signs (%) in the command, unless escaped with backslash \, will be changed into newline characters, and all data after the first % will be sent to the command as standard input.

![](bbox=[0.13, 0.45, 0.24, 0.56])

# **NOTE**

> The day of a command’s execution can be specified by two fields -- day of month, and day of week. If both fields are restricted (ie, aren't*), the command will be run when *either* field matches the current time. For example, “`30 4 1,15 * 5`” would cause a command to be run at 4:30 am on the 1st and 15th of each month, plus every Friday.

# # EXAMPLE CRON FILE

```
# use /bin/sh to run commands,no matter what /etc/passwd says
SHELL=/bin/sh
# mail any output to 'paul', no matter whose crontab this is
MAILTO=paul
#
# Run five minutes after midnight, every day
5 0 * * * $HOME/bin/daily.job >> $HOME/tmp/out 2>&1
# run at 2:15pm on the 1st of month -- output mailed to paul
15 14 1 * * $HOME/bin/monthly
# run at 1-5 pm on weekdays, annoy Joe
0 22 * * 1-5 mail -s 'It's 10pm' joe%Where%are%your%kids%
23 0-23/2 * * * echo 'run 23 mins after midn, 2, 4,..., daily'
5 4 * * sun echo 'run at 5 after 4 every sunday'
```