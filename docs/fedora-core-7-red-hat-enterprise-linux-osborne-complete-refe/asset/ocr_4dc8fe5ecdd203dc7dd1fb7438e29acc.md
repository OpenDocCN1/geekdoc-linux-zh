576 Part VI: System Administration

# The cron.d Directory

On a heavily used system, the /etc/crontab file can become crowded easily. There may also be instances where certain entries require different variables. For example, you may need to run some task under a different shell. To help better organize your crontab tasks, you can place crontab entries in files within the cron.d directory. The files in the cron.d directory all contain crontab entries of the same format as /etc/crontab. They may be given any name. They are treated as added crontab files, with cron checking them for tasks to run.

For example, Fedora installs a smolt file in the cron.d that contains crontab entries to run system statistics for the SMOLT hardware reporting service.

# The crontab Command

You use the crontab command to install your entries into a crontab file. To do this, first create a text file and type your crontab entries. Save this file with any name you want, such as mycronfile. Then, to install these entries, enter crontab and the name of the text file. The crontab command takes the contents of the text file and creates a crontab file in the /var/spool/cron directory, adding the name of the user who issued the command. In the following example, the root user installs the contents of mycronfile as root’s crontab file. This creates a file called /var/spool/cron/root. If a user named justin installed a crontab file, it would create a file called /var/spool/cron/justin. You can control use of the crontab command by regular users with the /etc/cron.allow file. Only users with their names in this file can create crontab files of their own. Conversely, the /etc/cron.deny file lists those users denied use of the cron tool, preventing them for scheduling tasks. If neither file exists, access is denied to all users. If a user is not in an /etc/cron.allow file, access is denied.

However, if the /etc/cron.allow file does not exist, and the /etc/cron.deny file does, then all users not listed in /etc/cron.deny are automatically allowed access.

```
# crontab mycronfile
```

# Editing in cron

Never try to edit your crontab file directly. Instead, use the crontab command with the -e option. This opens your crontab file in the /var/spool/cron directory with the standard text editor, such as Vi—crontab uses the default editor as specified by the EDITOR shell environment variable. To use a different editor for crontab, change the default editor by assigning the editor’s program name to the EDITOR variable and exporting that variable. Normally, the editor variable is set in the /etc/profile script. Running crontab with the -l option displays the contents of your crontab file, and the -r option deletes the entire file. Invoking crontab with another text file of crontab entries overwrites your current crontab file, replacing it with the contents of the text file.

# Organizing Scheduled Tasks

You can organize administrative cron tasks into two general groups: common administrative tasks that can be run at regular intervals, and specialized tasks that need to be run at a unique time. Unique tasks can be run as entries in the /etc/crontab file, as described in the next section. Common administrative tasks, though they can be run from the /etc/crontab file, are better organized into specialized cron directories. Within such directories, each task