# Identifying Running Daemons

If you want to stop or reconfigure a daemon that's already running, the first step is to find that daemon's process identification (PID) number. This information can be most easily obtained by using the ps command in conjunction with grep. For instance, suppose I want to find the PID of the smbd (Samba) program. I could type ps ax | grep smbd - at a Linux command prompt, and the system would reply with something like this:

```
653 ? S 0:00 [smbd]
16017 pts/9 S 0:00 grep smbd -
```

The second line is the grep command used to get the output itself, and can be ignored. The first lists the smbd program. At the beginning of that line is the PID—653 in this case. You'll need to use this number to refer to the program when stopping it.

If you don't recall the exact name of the daemon, you can use whatever part of it you do remember, or omit the grep component of the command entirely (that is, just type ps ax). This will increase the number of entries you'll see on your screen, however, making it more difficult to locate the program you want to stop or restart.

In the case of daemons that are invoked by inetd, you may need to modify /etc/inetd.conf and restart inetd instead of directly starting, stopping, or restarting the target daemon. If such a daemon is currently working (say, if smbd had been launched from inetd, and if Windows machines were still accessing Linux shares), it might be necessary to kill that daemon directly, in addition to modifying /etc/inetd.conf. (Stopping a running daemon will, however, disconnect anybody who's currently using it.)

# Stopping Daemons

You use the Linux kill command to stop a daemon (or any other program). For instance, to stop the smbd daemon identified earlier, you would type kill 653. Sometimes a program won't stop when you kill it this way, but adding a -9 parameter before the PID usually does the trick, as in kill -9 653. You should repeat the ps command to be sure that the kill command worked; if it did work, the daemon won't be listed in the output.

If you simply wanted to eliminate a daemon, you can stop here (unless you want to prevent it from starting up when you restart your computer, in which case you'll need to modify /etc/inetd.conf, /etc/rc.d/rc.local, or some other file that launches it automatically). If you want to modify the daemon's actions, you can start it again with modified parameters, or modify its configuration file.

# Starting Daemons

You can start a daemon by typing its name at a command prompt. You may need to include a complete path to the executable file, as in /usr/sbin/smbd to start smbd. Like other programs, daemons often take parameters to modify their behavior, and you can include any parameters