When init receives a SIGPWR signal, and a file called /etc/powerstatus contains an OK string, the powerokwait action is activated.

# # Managing init Files

As you already know, System V init uses a lot of files, symbolic links, and directories. To simplify management of init files, a few tools are available. This section discusses two such commonly used tools.

# ## Using chkconfig to manage run levels

The chkconfig utility enables you to maintain the various symbolic links necessary for starting and stopping services in a run level. This utility can manage run level configuration for all the scripts in the /etc/rc.d/init.d directory. Its uses are described next.

# ### Listing manageable services

To view what services will start or stop in what run levels, run the following command:

```
chkconfig --list
```

This command lists all the chkconfig-manageable services and tells what services are going to be started (on) or stopped (off) for each run level. You can also check to see the run level configuration for a particular service by specifying the service name (that is, the script name in /etc/rc.d/init.d) in the command line. For example,

```
chkconfig --list httpd
```

shows the following output in an example Red Hat Linux server:

```
httpd  0:off  1:off  2:off  3:on  4:on  5:on  6:off
```

The httpd service is on for run levels 3, 4, and 5 and is off for levels 0, 1, 2, and 6.