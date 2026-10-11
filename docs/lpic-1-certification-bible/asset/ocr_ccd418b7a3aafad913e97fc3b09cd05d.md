+   11. D. Differential backups are used to back up files that have changed since the last full backup. See the “Differential backup” section for more information.

+   12. B. The `cpio` utility will copy files from an archive when used in the copy-out mode. See the “Using the cpio utility” section for more information.

+   13. A. The `tar` utility can use the `gzip` utility to automatically compress and uncompress files during file creation. See the “Using the tar utility” section for more information.

+   14. C. The log file containing login times for users is stored in `\var/log/lastlog` by default. See the “Configuring system logging” section for more information.

+   15. `logrotate`. The `logrotate` command is used to rotate system logs. See the “Rotating system logs” section for more information.

+   16. A. The `gunzip` utility can compress files created with `gzip` and `compress`. See the “Using the gunzip utility” section for more information.

+   17. C. The `cron -l` command is used to display the current contents of `crontab`. See the “Using the cron daemon” section for more information.

+   18. D. The \- character increases the speed of system logging by not syncing the log after each write. See the “Configuring system logging” section for more information.

+   19. B. The `kernel.h` file is used to specify the message levels that are displayed using `dmesg`. See the “Identifying problems using log files” section for more information.

+   20. C. Core dump files can be viewed using the GNU Debugger or `gdb`. See the “Limiting Core Dump Files” section for more information.

# Scenarios

+   1. Using the boot log you can see which hardware was detected and which device files they were associated with. Most likely you would use `dmesg | more or dmesg | grep`.

+   2. The easiest solution is to use a combination of `cron` and `tar`. Use `cron` to execute the job every night and `tar` to do the backup. By using the `-u` option with `tar` you can do a differential backup every night and a full backup on the weekends. With some minor scripting you can also use `gzip` to compress the archive to make it smaller.

+   3. The first step is to note any accounts that you do not want to delete, even though they may not have been logged in recently. Some daemons use special accounts that are not shown as logged in. After that, you can use the `lastlog` command to see when the last login was for an account.