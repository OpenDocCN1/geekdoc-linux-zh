# Listing manageable services

To view what services will start or stop in what run levels, run the following command:

```
chkconfig --list
```

This command lists all the chkconfig-manageable services and tells you what services are going to be started (on) or stopped (off) for each run level. You can also check to see the run level configuration for a particular service by specifying the service name (that is, the script name in /etc/rc.d/init.d) in the command line. For example,

```
chkconfig --list httpd
```

shows the following output in an example Red Hat Linux server:

```
httpd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

The httpd service is on for run levels 2, 3, 4, and 5 and is off for levels 0, 1, and 6.

# Adding a new service

If you just added a new script in the /etc/rc.d/init.d directory and want to make the service it offers available for a particular run level, you can run the chkconfig command as follows:

```
chkconfig --add service_name [--level runlevel]
```