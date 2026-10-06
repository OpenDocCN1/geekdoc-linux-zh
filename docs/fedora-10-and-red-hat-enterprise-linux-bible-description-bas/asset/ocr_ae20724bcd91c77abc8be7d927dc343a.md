# Part III: Administering Fedora and RHEL

The file automatically opens in the text editor that is defined in your EDITOR or VISUAL environment, vi as the default. When you're done, simply exit the editor. Provided there were no syntax errors, your crontab file will be installed. For example, if your user name is jsmith, you have just created the file /var/cron/jsmith. If you add a line (with a descriptive name, of course) to remove any old core files from your source directories, that file may look like this:

```
# Find and remove core files from /home/jsmith/src
5 1 * * * Sun find /home/jsmith/src -name core.[0-9]* -exec rm {} \ /dev/null 2>&1
```

Because core files in Fedora and RHEL consist of the word core, followed by a dot (.) and process ID, this example will match all files beginning with core. and by a number. The root user can access any user's individual crontab file by using the -u username option to the crontab command.

# cron files

Separate directories are set up to contain cron jobs that run hourly, daily, weekly, and monthly. These cron jobs are all set up to run from the /etc/crontab file. The default ///ontab file looks like this:

```
SHELL=/bin/bash
PATH=/bin:/usr/sbin:/usr/bin
MAILTO=root
=
# run-parts
01 * * * run-parts /etc/cron.hourly
02 4 * * * run-parts /etc/cron.daily
22 4 * * run-parts /etc/cron.weekly
42 4 1 * * run-parts /etc/cron.monthly
```

The first lines initialize the run-time environment for all subsequent jobs (the shell in which jobs run, the executable search path, the recipient of output and error messages, and user's home directory). The next five lines (as the user root) the run-parts program controls what you may want to run periodically.

run-parts is a script that takes a directory as a command-argument. It sequentially runs every program within that directory (shell scripts are most common, but binaries and links are also evaluated). The default configuration executes programs in /etc/cron.hourly at one minute every hour of every day;/etc/cron.daily at 4:02 a.m. every day; on Sundays and /etc/cron.monthly at 4:42 a.m. on the first day of each month.