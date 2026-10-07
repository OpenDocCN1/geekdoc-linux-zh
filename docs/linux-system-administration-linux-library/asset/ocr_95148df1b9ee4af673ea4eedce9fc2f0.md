# Initialization and Startup Scripts

You'll notice that each file begins with an S or a K. The system first runs the scripts names start with K to kill their associated processes, if running. Next, the system runs the scripts whose names start with S to start the associated processes. Changing a K name to start with S (such as renaming k20fs to s20fs) makes Linux start the process rather than kill it when entering the run level, and changing an S to K causes Linux to the process when exiting the run level. This is how Linux controls what processes start in a given run level.

![](bbox=[0.893, 0.115, 0.953, 0.246])

After the run level 3 processes are killed or started, the /sbin/update command in the inittab file is run. This command flushes the kernel buffers and writes their data to the hard drive. This is basic housekeeping to improve kernel performance.

The next line sets the Ctrl+Alt+Delete key combination to initiate a reboot of the system. The -t option indicates that the init process is to wait 3 seconds before telling its dependent processes to restart themselves. The shutdown occurs as if you had initiated the following shutdown command:

```
# /sbin/shutdown -t3 -r now
```

The pr line of the inittab file sets the system up to run a different kind of shutdown if an attached uninterrupted power supply (UPS) indicates that process has failed. The shutdown is to occur 2 minutes after this notification. The pr line, however, indicates that the shutdown is to be cancelled if the init process receives a notification that the power was restored before the shutdown was initiated.

The next uncommented lines, with identifiers 1-6, run getty programs for the virtual terminals. These getty programs are essential since they initialize the tty, provide the login and retrieve the user-input data, and start a login process for the user. Without these lines, no users could log into the system.

The last line, with the identifier of x, is set by the 5 in the second colon-delimited field to run the X Display Manager (XDM) process for run level 5. An XDM allows you to log into run level 5 directly. Red Hat 7.0 uses predm as its XDM process, but the program varies from one to another.

If /etc/inittab contained any additional lines that specified no run level (meaning to run at boot time only) or run level 3, they would be run. You can add any such lines yourself, if you have something that you need to start only in a certain run level. Usually the Red Hat default inittab is fine as it comes.

After running /etc/inittab, the system turns its attention to the rc.sysinit script, which performs many functions. These include:

+   - Setting the path and the hostname, and checking whether networking is activated

+   - Mounting the /proc filesystem