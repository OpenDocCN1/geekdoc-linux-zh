column. For example, if a Firefox process has a TIME field greater than 100.0, the process has likely run upon. However, if the user is doing a lot of Java work and has not logged out for a long time, this value may be normal. Look at the STIME field to see when the process was started. If the process has been running for longer than the user has logged in, it is a good candidate to be killed.

When a user gets stuck and leaves their terminal unattended without notifying anyone, it is convenient to kill (page 455) all processes owned by that user. If the user is running a system process, such as GNOME or KDE on the console, kill the will window manager process. Manager processes to look for include starttk, x-session-manager, or another process that ends in wm. Usually the window manager is either the first or last thing to be, and exiting from the window manager logs the user out. If killing the window manager does not work, try killing the X server process. This process is typically listed as /usr/bin/X or /usr/X11R/bin/X. If that fails, you can kill all processes owned by a user by giving the command -TERM -15 or, equivalently, -TERM -1 while you are logged in as user. Using -1 (one) in place of the PID tells will send the signal to all processes that are owned by that user. For example, you could give the following command:

```
$ sudo -u zach killall -TERM -1
```

If this does not kill all processes (sometimes TERM does not kill a process), you can use the KILL signal (-). The following line will definitely kill all processes owned by Zach and will not be friendly about:

```
$ sudo -u zach killall -KILL -1
```

If you do not include -u zach, this command brings the system down.

# # lsof: Finds Open Files

The lsof (list open files) utility displays the names of open files. Its options only certain processes, only file descriptors of a process, or only certain connections (network connections use file descriptors as normal files and lsof can show them as well). Once you have identified a suspect process using -cf, give the following command:

```
$ sudo lsof -p pid
```

Replace pid with the process ID of the suspect process; lsof displays a list of descriptors that pid has open. The -s option displays the sizes of all open files and the -p option allows you to specify the PID number of process of interest. This size information is helpful in determining whether the process has a very large open file. If it does, contact the owner of the process or, if necessary, kill the process. The -n option redisplays the output of lsof every n seconds.

# # KEEPING A MACHINE LOG

A machine log that includes the information shown in Table 16-3 can help you find and fix system problems. Note the time and date for each entry in the log. Avoid the