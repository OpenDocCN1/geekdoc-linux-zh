information on **xinetd**. Send a SIGHUP2 signal to reload **xinetd**. Red Hat Linux makes this simple using the following command:

```
`[root@tedford /root]# service xinetd reload`
```

![](bbox=[0.13, 0.21, 0.22, 0.25])

# NOTE

If you have a system using the older **inetd**, edit the */etc/inetd.conf* file and comment out the service you no longer want. To designate the service as a comment, start the line with a number sign (#). Remember to send the HUP signal to **inetd** once you've made any changes to the */etc/inetd.conf* file.

# ## Shutting Down Non-xinetd Services

If a service is not run by **xinetd**, then a process that is probably started at boot time is running it. The easiest way to stop that from happening is to edit the startup service list using the **redhat-config-services** GUI tool or the **ntsysv** command from the command line as described in Module 8. You can also manually change the symlink. Go to the */etc/rc.d/* directory and in one of the *rc*.d directories, find the symlinks that point to the startup script. (See Module 8 for information on startup scripts.) Rename the symlink to start with an X instead of S. Should you decide to restart a service, it's easy to rename it again starting with an S. If you have renamed the startup script but want to stop the currently running process, use the **service** command to tell the process to **stop**. For example, here is the command to kill a **portmap** process:

```
`[root@tedford /root]# service portmap stop`
```

![](bbox=[0.13, 0.61, 0.22, 0.65])

# NOTE

As always, be sure of what you're killing before you kill it, especially on a production server.

# ## A Note about the syslogd Service

One non-**inetd** service that will pop up on **netstat** output but can be safely ignored is **syslogd**. This service has historically defaulted to binding to a network port and listening for network messages to log. Because of the danger of logging arbitrary messages from a network, Linux developers have added a mechanism whereby **syslogd** logs requests sent from other hosts only if it has been started with the `--r` option. By default, **syslogd** does not start with `--r`, so you can safely let it remain on your system.