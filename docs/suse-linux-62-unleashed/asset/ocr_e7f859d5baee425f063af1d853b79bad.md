# Top Linux Commands and Utilities
APPENDIX C

off of that. Because the root directory is /usr/ftp, the ftp program will actually put thenuser in the /usr/ftp/etc directory (assuming there is one).

The syntax for the command follows:

```
chroot <new filesystem location> <command>
```

# chsh

You can use this program to change the type of shell you use when you log in to your Linux
system. The shell must be available on the system and must be allowed by the root
operator by its name listed in the /etc/shells file. Type the name of a shell,
following the chsh command:

```
# chsh zsh
```

# cp

The cp command is an abbreviation for copy; therefore, this command enables you to copy
objects. For example, to copy the file file1 to file2, issue the following command:

```
# cp file1 file2
```

As the example shows, the syntax is very simple:

```
cp <original object name> <new object name>
```

# cpio

The cpio command copies files in and out of file archives. cpio works like the tar
(tape archive) command, but with a slightly different syntax. Many SuSE Linux users are
more familiar with the tar command.

# cron

This is the cron daemon. This program, started when you first boot Linux, scans the /etc/
crontab file and the /var/cron/tabs directory.

# crontab

The crontab command, not to be confused with the /etc/crontab file, is used by your
system's users to schedule personal cron events. The cron events are stored in a directory
with the user's name under the /var/cron/tabs directory. By default, SuSE Linux allows
users to create cron jobs. All current jobs are listed when the crontab command is used
with the -l option. Use the -e to create or edit a job and the -r option to delete a
job.

![](bbox=[0.843, 0.452, 0.953, 0.603])