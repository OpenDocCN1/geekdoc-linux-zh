If the command is preceded by a K, the daemon is killed; if it is preceded by an S, the daemon is started. The numbers are used to order things—S30amd is started before S981ocal, for example.

The really nice thing about the system is the `/etc/rc.d/init.d/` directory. If you want to start and stop system services after everything is up and running, you don't have to look around anywhere, you can just do this:

```
$ /etc/rc.d/init.d/ntop stop
$
$ /etc/rc.d/init.d/ntop start
```

Now if you desire to change what and how things start at system boot, all you have to do is either change the ordering in the `/etc/rc.d/rcN.d` directories or change an S to a K. The configuration files for the scripts in `/etc/rc.d/init.d` are stored in `/etc/sysconfig/daemons`. By altering things in those directories, you can completely change how the system boots by hand.

Of course, you should know that altering those files is a wonderful way of rendering your system completely unbootable until some nice Linux guru comes by to fix it for you. That said, there is a remarkable amount of power and control concentrated among those few programs, so it is certainly good to know how it all works. You'll never become a Linux guru yourself without knowing.

# ## Task Scheduling

One of the conveniences of Linux and UNIX systems is how easy it is to schedule the system to do work when you aren't there. Many tasks are set up by the system to take care of things in the middle of the night when they won't bother you. You can also take advantage of this. Most of this scheduling is done using two programs: cron.tab and at. cron.tab is the user interface to the cron daemon. The cron daemon runs all the time and reads system and user configuration files to determine when it has a job to run. Using cron.tab, you can schedule programs for cron to run at any time in the future and at regular intervals.

If you just run the cron.tab program, it will start up an editor for you to write your schedule with. You can also feed it a file directly that already has your schedule in it. You can list your file with the -l option and change your editor with the -e option. Personal crontabs created with the crontab program have the following syntax:

| [minute] | [hour] | [day of month] | [month] | [day of week] | [command to run] |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0-59 | 0-23 | 0-31 | 0-12 [or name] | 0-7 [or name] | |