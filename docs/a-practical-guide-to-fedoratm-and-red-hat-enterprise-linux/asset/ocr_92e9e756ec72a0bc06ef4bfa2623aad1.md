Backing up files on the system is a critical but often-overlooked part of system administration. Linux includes the `tac`, `cpio`, `dump`, and `restore` utilities to back up and restore files. You can also use more sophisticated packages such as `amanda` and various commercial products.

The system scheduling daemon, `crond`, periodically executes scheduled tasks. You can schedule tasks using `crontab`, `anacrontab`, and `at`.

System reports present information on the health of the system. Two useful tools that generate these reports are `vmstat`, which details virtual memory, I/O, and CPU usage, and `top`, which reports on how the system is performing from moment to moment and can help you figure out what might be slowing it down.

Another aspect of system administration is solving problems. Linux includes several tools that can help track down system problems. One of the most important of these tools is `rsyslogd`, the system log daemon. Using `/etc/rsyslog.conf`, you can control which error messages appear on the console or a user’s terminal, which are sent to a remote system, and which go to one or several log files.

# ## EXERCISES

+   1. How would you list all the processes running `vi`?
+   2. How would you use `kill` to log Max off the system?
+   3. From the command line, how would you create a user named John Doe who has the username `jd` and who belongs to group `65535`?
+   4. Which problem does `logrotate` solve? Which is the primary configuration file for `logrotate`?
+   5. Give a command that creates a `gzip` compressed `tar` backup of the `/usr` filesystem on `/dev/sdg`. Which command would you use to make the same backup using `bzip2`? Using `cpio`?

# ## ADVANCED EXERCISES

+   6. If the system is less responsive than normal, what is a good first step in figuring out where the problem is?
+   7. A process stores its PID number in a file named `process.pid`. Write a command line that terminates this process.
+   8. Working with `root` privileges, you are planning to delete some files but want to make sure that the wildcard expression you use is correct. Suggest two ways you could make sure you delete the correct files.