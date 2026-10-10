![](bbox=[0.145, 0.085, 0.685, 0.365])

# Starting and Stopping Daemons Manually

Recall from the preceding section that the init daemon starts daemons at system initialization as well as starts and stops daemons afterwards when the runlevel is changed by executing the rc scripts within the /etc/init.d directory. To manipulate daemons after system startup, you can execute them directly from the /etc/init.d directory with the appropriate argument (start, stop, or restart). For example, to restart the cron daemon, you could run the following command:

```
[root@server1 ~]# /etc/init.d.cron restart
cron stop/waiting
cron start/running, process 3371
[root@server1 ~]# _
```

You can also use the service command to start, stop, or restart any daemons listed within the /etc/init.d directory. For example, you can restart the cron daemon using the following command:

```
[root@server1 ~]# service cron restart
cron stop/waiting
cron start/running, process 3352
[root@server1 ~]# _
```

The upstart init system also provides the stop command to stop a daemon, the start command to start a daemon, and the restart command to restart a daemon. Thus, you could also restart the cron daemon using the following command:

```
[root@server1 ~]# restart cron
cron start/running, process 3389
[root@server1 ~]# _
```

# Configuring Daemons to Start in a Runlevel

If your Linux distribution uses the upstart init system, then configuring a daemon to start or stop in a particular runlevel is as easy as modifying the associated daemon configuration file in the /etc/init directory, as shown earlier.