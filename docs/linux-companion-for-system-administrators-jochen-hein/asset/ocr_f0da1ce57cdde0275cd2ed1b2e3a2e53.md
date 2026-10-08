# 286 UNIX TOOLS

Besides the time of day, you can also specify the date on which at is to start the command. The date can be specified as DD.MM. YY or MM/DD/YY. Time specifications can also be indicated relative to the current time of day or the current date. If, for example a command is to be started in two hours' time, you can write this as +2 hours. With +2 days, you can start a command in two days' time.

The at command usually reads the commands to be executed from the standard input. However, you can also specify a file (shell script) by setting the option -f file. If the command to be executed writes to the standard error output, this output is sent via Unix to the user who triggered the at command.

The system administrator can control the at command by means of the two files /etc/at.allow and /etc/at.deny. If the file /etc/at.allow exists, only the users who listed in this file execute the at command. If this file does not exist, but the file /etc/at.deny is present, all users may use the at command except those listed in /etc/at.deny. If neither file exists, only the system administrator (root) is allowed to use the at command.

# 10.4.2 Simulating batch processing with batch

The at program executes the given command at the specified time in practically all circumstances. If the computer's system load at time is extremely high, it would be better to prevent execution of the process or move it to a different time. The batch command schedules a program in the same way as at, but only executes if the computer's load allows it. Otherwise, the handling is the same as the at command.

# 10.4.3 Executing commands periodically (crontab)

The at command executes a command only once. If given commands are to be executed regularly at specific times, they can be entered in the crontab table. This is done by using the homonymous command crontab. With crontab, periodically executed routine tasks can be carried out automatically. Examples of such tasks are generation of index files, monitoring the system on the basis of various criteria, or deletion of log files.

The crontab tables created with the crontab are stored in the directory /var/cron/tabs. These files must not be modified directly, but should be edited by means of the crontab command with the option -e. This starts the editor specified in the environment variable EDITOR with the current