# xinetd Servers

To start the server only when a request for its services is received, you configure it using the xinetd daemon. If you add, change, or delete server entries in the /etc/xinetd files, you will have to restart the xinetd daemon for these changes to take effect. On Red Hat, you can restart the xinetd daemon using the /etc/rc.d/init.d/xinetd script with the restart argument, as shown here:

```
# service xinetd restart
```

You can also use the xinetd script to start and stop the xinetd daemon. Stopping effectively shuts down all the servers that the xinetd daemon manages (those listed in the /etc/xinetd.conf file or the xinetd.d directory).

```
# service xinetd stop
# service xinetd start
```

You can also directly restart xinetd by stopping its process directly. To do this, you use the killall command with the -HUP signal and the name xinetd.

```
# killall -HUP xinetd
```

Tip Versions prior to Red Hat 7.0 used the inetd daemon (the term stands for the Internet Services Daemon) instead of xinetd. xinetd is meant to be the enhanced replacement for inetd. If you are upgrading from inetd, you can use the inetdconvert command to convert inetd entries into xinetd configurations.