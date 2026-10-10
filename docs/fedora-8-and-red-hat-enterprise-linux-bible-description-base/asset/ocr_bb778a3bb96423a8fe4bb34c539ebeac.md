```
```
# service smb stop
Shutting down SMB services:         [  OK  ]
```
```

The smb run-level script is different from other run-level scripts in that it supports several other options than *start* and *stop*. For example, this script has options (not shown in the example) that allow you to reload the `smb.conf` configuration file (*reload*) and check the status of the service (*status*).

# ## Changing run-level script behavior

Modifying the startup behavior of any such script merely involves opening the file in a text editor. For example, the `atd` daemon queues jobs submitted from the `at` and `batch` commands. Jobs submitted via `batch` are executed only if the system load is not above a particular value, which can be set with a command-line option to the `atd` command.

The default *limiting load factor* value of 0.8 is based on the assumption that a single-processor machine with less than 80 percent CPU utilization could handle the additional load of the batch job. However, if you were to add another CPU to your machine, 0.8 would only represent 40 percent of the computer’s processing power. So you could safely raise that limit without impacting overall system performance.

You can change the limiting load factor from 0.8 to 1.6 to accommodate the increased processing capacity. To do this, simply modify the following line (in the *start* section) of the `/etc/init.d/atd` script:

```
```
daemon /usr/sbin/atd
```
```

Replace it with this line, using the -1 argument to specify the new minimum system load value:

```
```
daemon /usr/sbin/atd -l 1.6
```
```

After saving the file and exiting the editor, you can reboot the machine or just run any of the following three commands to begin using the new batch threshold value:

```
```
# service atd reload
# service atd restart
# service atd stop ; service atd start
```
```

> **NOTE:** Always make a copy of a run-level script before you change it. Also, keep track of changes you make to run-level scripts before you upgrade the packages they come from. You need to make those changes again after the upgrade.

If you are uncomfortable editing startup scripts and you simply want to add options to the daemon process run by the script, there may be a way of entering these changes without editing the startup script directly. Check the `/etc/sysconfig` directory and see if there is a