
## Changing run-level script behavior

Modifying the startup behavior of any such script merely involves opening the file in a text editor.

For example, the atd daemon queues jobs submitted from the at and batch commands. Jobs submitted via batch are executed only if the system load is not above a particular value, which can be set with a command-line option to the atd command.

The default limiting load factor value of 0.8 is based on the assumption that a single-processor machine with less than 80 percent CPU utilization could handle the additional load of the batch job. However, if you were to add another CPU to your machine, 0.8 would only represent 40 percent of the computer’s processing power. So you could safely raise that limit without impacting overall system performance.

This load limit is set in a file of options for the atd daemon. You can find out which file by looking into the /etc/init.d/atd script. After the initial comments near the top, you’ll see lines like the following:

```
prog="atd"
[ -e /etc/sysconfig/$prog ] && . /etc/sysconfig/$prog
```

These lines check for the existence of the file /etc/sysconfig/atd, and if the file exists, sources in the commands (and settings) in that file.

In the /etc/sysconfig/atd file, you’ll see a commented out set of options:

```
#example
#OPTS="-l 4 -b 120"
```

Notice how the example shows a load level of 4.

You can change the limiting load factor to 1.6 to accommodate the increased processing capacity. To do this, simply modify the OPTS line:

```
#OPTS="-l 4 -b 120"
```

Remove the comment marker, #, and then set the value you want after the -l option, to specify the new minimum system load value:

```
OPTS="-l 1.6 -b 120"
```

After saving the file and exiting the editor, you can reboot the machine or just run any of the following three commands to begin using the new batch threshold value:

```
# service atd reload
# service atd restart
# service atd stop ; service atd start
```

> **NOTE:** Always make a copy of a run-level script before you change it. Also, keep track of changes you make to run-level scripts before you upgrade the packages they come from. You need to make those changes again after the upgrade.

Many of the startup scripts use a file in the /etc/sysconfig directory to set their options, similar to the atd script. Check the /etc/sysconfig directory and see if there is a file by the same name as the script you want to modify. If there is, that file probably provides values that you can set to pass options to the startup script. Sysconfig files exist for atd, crond, dhcpd, ntpd, samba, squid, and others.

### Reorganizing or removing run-level scripts

There are several ways to deal with removing programs from the system startup directories, adding them to particular run levels, or changing when they are executed. From a Terminal window, you can use the chkconfig command. From a GUI, use the Service Configuration window.

> **CAUTION:** You should never remove the run-level file from the /etc/init.d directory. Because no scripts are run from the /etc/init.d directory automatically, it is okay to keep them there. Scripts in /etc/init.d are only accessed as links from the /etc/rcX.d directories. Keep scripts in the init.d directory so you can add them later by re-linking them to the appropriate run-level directory.

To reorganize or remove run-level scripts from the GUI, use the Service Configuration window. Either select System → Administration → Services or log in as root user and type the following command in a Terminal window:

```
# system-config-services &
```

Figure 11-1 shows an example of the Service Configuration window.

The Service Configuration window enables you to reconfigure services for run levels 2, 3, 4, and 5. Icons next to each service indicate whether the service is currently enabled (green) or disabled (red) for the current run level and whether or not the service is currently running. Select a service to see a description of that service. Here is what you can do from this window:

- **Enable** — With a service selected, click the Enable button to enable the service to start when you start your computer (run levels 2, 3, 4, and 5).
- **Disable** — With a service selected, click Disable to have the service not start when you boot your computer (or otherwise enter run levels 2, 3, 4, or 5).
- **Customize** — With a service selected, click Customize and select the run levels at which you want the service to start.
- **Start** — Click a service on the list. Select Start to request the service to immediately start.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_489_0.png)

Some administrators prefer text-based commands for managing run-level scripts and for managing other system services that start automatically. The chkconfig command can be used to list whether services are configured to be on or off. To see a list of all system services, with indications that they are on or off, type the following:

```
# chkconfig --list | less
```

You can then page through the list to see those services. If you want to view the status of an individual service, you can add the service at the end of the list option. For example, to see whether the nfs service starts in each run level, type the following:

```
# chkconfig --list nfs
nfs        0:off  1:off  2:on  3:on  4:on  5:on  6:off
```

This example shows that the nfs service is set to be on for run levels 2, 3, 4, and 5, but that it is set to off for run levels 0, 1, and 6.

Another tool that can be run from the shell to change which services start and do not start at various levels is the ntsysv command. Type the following as root user from the shell:

```
# ntsysv
```

A screen appears with a list of available services. Use the up and down arrow keys to locate the service you want. With the cursor on a service, press the Spacebar to toggle the service on or off. Press the Tab key to highlight the OK button, and press the Spacebar to save the change and exit. The ntsysv tool only changes services for the current run level. You can run ntsysv several times with different run levels active (see Section 11.1) to set services on different levels. For example, type the following:

ntsysv with the `--level #` option, where `#` is replaced by the run level for which you want to change services.

## Adding run-level scripts

Suppose you want to create and configure your own run-level script. For example, after installing the binaries for the fictitious my_daemon program, it needs to be configured to start up in run levels 3, 4, and 5 and terminated in any other run level. You can add the script to the `/etc/init.d` directory, and then use the chkconfig command to configure it.

To use chkconfig, ensure that the following lines are included in the `/etc/init.d/my_daemon` script:

```
#!/bin/sh
#
# Service my_daemon starts and stops the my_daemon daemon
#
# chkconfig: 345 82 28
# description: Starts the my daemon daemon, \
     nicely.
#
### BEGIN INIT INFO
# Provides: my_daemon
# Required-Start: $local_fs
# Required-Stop: $local_fs
# Default-Start: 3 4 5
# Default-Stop: 0 1 2 6
# Short-Description: Start/stop the "my_daemon" daemon
# Description:     Runs commands scheduled by the "my_daemon"
#      and provides a chkconfig example.
### END INIT INFO
```

> **NOTE:** The line chkconfig: 345 82 28 sets the script to start in run levels 3, 4, and 5. It sets start scripts to be set to 82 for those run levels. It sets stop scripts to be set to 28 in all other levels.

You need both the old-style chkconfig lines at the top and the newer-style LSB (Linux Standard Base) init information blocks as comments in your script. The init information block takes precedence over the information at the top of the file as well.

In this case, the default start levels are 3, 4, and 5.

> **NOTE:** You will see quite a variation in the information in the default set of /etc/init.d scripts. If chkconfig detects problems, but still has enough information to set up your service, you will likely end up with a service that is off for each run level.

With those lines in place, simply run the following command:

```
# chkconfig --add my_daemon
```
