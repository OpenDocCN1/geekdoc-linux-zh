/usr/sbin and /sbin. MAILTO designates to whom the results of a task are to be mailed. By default, these are mailed to the user who schedules it, but you can have the results sent to a specific user, such as the administrator's e-mail address, or an account on another system in a network. HOME is the home directory for a task, in this case the top directory.

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/
```

# cron.d Directory

On a heavily used system, the /etc/crontab file can become crowded easily. There may also be instances where certain entries require different variables. For example, you may need to run some task under a different shell. To help better organize your crontab tasks, you can place crontab entries in files within the cron.d directory. The files in the cron.d directory all contain crontab entries of the same format as /etc/crontab. They may be given any name. They are treated as added crontab files, with cron checking them for the task to run. For example, Red Hat installs a sysstat file in the cron.d that contains crontab entries to run tools to gather system statistics.

# crontab Command

You use the crontab command to install your entries into a crontab file. To do this, first create a text file and type your crontab entries. Save this file with any name you want, such as mycronfile. Then, to install these entries, enter crontab and the name of the text file. The crontab command takes the contents of the text file and creates a crontab file in the /var/spool/cron directory, adding the name of the user who issued the command. In the following example, the root user installs the contents of the mycronfile as the root's crontab file. This creates a file called /var/spool/cron/root. If a user named justin installed a crontab file, it would create a file called /var/spool/cron/justin. You can control use of the crontab command by regular users with the /etc/cron.allow file. Only users with their names in this file can create crontab files of their own. Conversely, the /etc/cron.deny file lists those users denied use of the cron tool, preventing them from scheduling tasks. If neither file exists, access is denied to all users. If a user is not in a /etc/cron.allow file, access is denied. However, if the /etc/cron.allow file does not exist, and the /etc/cron.deny file does, then all users not listed in /etc/cron.deny are automatically allowed access.

```
# crontab mycronfile
```

# cron Editing

Never try to edit your crontab file directly. Instead, use the crontab command with the -e option. This opens your crontab file in the /var/spool/cron directory with the standard text editor, such as Vi. crontab uses the default editor as specified by the EDITOR shell environment variable. To use a different editor for crontab, change the default editor by assigning the editor's program name to the EDITOR variable and exporting that variable. Normally, the editor variable is set in the /etc/profile script. Running crontab with the -l option displays the contents of your crontab file, and the -r option deletes the entire file. Invoking crontab with another text file of crontab entries overwrites your current crontab file, replacing it with the contents of the text file.

# Organizing Scheduled Tasks

You can organize administrative cron tasks into two general groups: common administrative tasks that can be run at regular intervals, or specialized tasks that need to run at a unique time. Unique tasks can be run as entries in the /etc/crontab file, as described in the next section. Common administrative tasks, though they can be run from the /etc/crontab file, are better organized into specialized cron directories. Within such directories, each task is placed in its own shell script that will invoke the task when run. For example, there may be several administrative tasks that all need to be run each week on the same day, say if maintenance for a system is scheduled on a Sunday morning. For these kinds of tasks, cron provides several specialized directories for automatic daily, weekly, monthly, and yearly tasks. Each contains a cron