# Appendixes
PART V

specify. This is a handy way to handle unwanted incoming mail or organize vast amounts
of incoming mail.

# ps

ps gives a snapshot of the current processes:

```
$ ps -ef

PID TTY STAT      TIME COMMAND
10916 p3 S       0:00 -bash TERM=vt100 HOME=/home2/dpitts
PATH=/usr/local/bin:/us
10973 p3 R       0:00 _ ps -ef LESSOPEN=|lesspipe.sh %s ignoreeeof=10
HOSTNAME=s
10974 p3 S       0:00 _ more LESSOPEN=|lesspipe.sh %s ignoreeeof=10
HOSTNAME=svr
```

# pwd

pwd prints the current working directory. It tells you what directory you are in currently.

# quota

The quota command reports on disk quota settings. This command, most used by the
root operator, shows how much disk space users can use by user or group.

# quotacheck

Gives a report on disk-quota usage. This command, most used by the root operator,
scans a specified or current filesystem, reporting on disk usage if disk quotas for users are
turned.

# quotaoff

quotaoff turns off disk quotas. This command is used by the root operator to disable disk-
quota checking for users.

# quotaon

quotaon turns on disk quotas. This command is used by the root operator to enable or
enforce disk quotas for users and can be helpful in limiting how much disk space a user can
take up with programs or data.