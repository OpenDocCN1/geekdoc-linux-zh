
## Service Management Tools: chkconfig and redhat-config-services

On Red Hat, redhat-config-services and the chkconfig command provide simple interfaces you can use to choose what servers you want started up and how you want them to run. You use these tools to control any daemon you want started up, including system services such as cron, the print server, remote file servers for Samba and NFS, authentication servers for Kerberos, and, of course, Internet servers for FTP or HTTP. Such daemons are referred to as services, and you should think of these tools as managing these services. Any of these services can be set up to start or stop at different runlevels.

These tools manage services that are started up by scripts in the /etc/rc.d/init.d directory. If you add a new service, both chkconfig and redhat-config-services can manage it. As described in the following section, services are started up at specific runlevels using startup links in various runlevel directories. These links are connected to the startup scripts in the init.d directory. Runlevel directories are numbered from 0 to 6 in the /etc/rc.d directory, such as /etc/rc.d/rc3.d for runlevel 3 and /etc/rc.d/rc5.d for runlevel 5. Removing a service from a runlevel only changes its link in the corresponding runlevel rc.d directory. It does not touch the startup script in the init.d directory.

### redhat-config-services

With the Red Hat redhat-config-services utilities, you can simply select from a list of commonly used services those that you want to run when your system boots up. You can access redhat-config-services from the Services icon in the Server Settings window or menu, located under System Settings. redhat-config-services lets you start, stop, and restart a server, much like the service command (see Figure 20-1). redhat-config-services provides a GNOME GUI interface for easy use. It displays a list of your installed servers, with checked check boxes for those currently chosen to start up. You can start, stop, or restart any particular service by selecting it and choosing either Start Service, Stop Service, or Restart Service from the Action menu.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_449_0.png)

Figure 20-1: redhat-config-services

You can also set startup runlevels for services, just as you can with chkconfig, though you are limited to levels 3, 4, and 5. The list of checked entries differs depending on the runlevel you choose from the Edit Runlevel menu. In effect, you are choosing which services to start at a given runlevel. The default is runlevel 5, the GUI startup level. You may want a different set of services started or stopped for runlevel 3, the command line startup level. In that case, you would select Runlevel 3 from the Edit Runlevel menu to display the services with selected check boxes for runlevel 3.

### chkconfig

You can specify the service you want to start and the level you want to start it at with the chkconfig command. Unlike other service management tools, chkconfig works equally well on standalone and xinetd Services. Though standalone services can be run at any runlevel, you can also turn xinetd services on or off for the runlevels that xinetd runs in. Table 20-3 lists the different chkconfig options.

### Listing Services with chkconfig

To see a list of services, use the --list option. A sampling of services managed by chkconfig are shown here. The on or off status of the service is shown at each runlevel. xinetd services and their status are also shown:

```
chkconfig --list
dhcpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
named 0:off 1:off 2:off 3:off 4:off 5:off 6:off
lpd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
nfs 0:off 1:off 2:off 3:off 4:off 5:off 6:off
crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
xinetd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
xinetd based services:
    time:      off
    finger:    off
    pop3s:     off
    swat:      on
```

### Starting and Stopping Services with chkconfig

You use the on option to have a service started at specified runlevels, and the off option to disable it. You can specify the runlevel to affect with the --level option. If no level is specified, chkconfig will use any chkconfig default information in a service's init.d startup script. Red Hat installs its services with chkconfig default information already entered (if this is missing, chkconfig will use runlevels 3, 4, and 5). The following example has the Web server (httpd) started at runlevel 5:

```
chkconfig --level 5 httpd on
```

Table 20-3: chkconfig Options

| Option | Description |
|---|---|
| --level runlevel | Specifies a runlevel to turn on, turn off, or reset a service. |
| --list service | Lists startup information for services at different runlevels. xinetd services are just on or off. With no argument, all services are listed, including xinetd services. |
| --add service | Adds a service, creating links in the default specified runlevels (or all runlevels, if none are specified). |
| --del service | Deletes all links for the service (startup and shutdown) in all runlevel directories. |
| service on | Turns a service on, creating a startup link in the specified or default runlevel directories. |
| service off | Turns a service off, creating shutdown links in specified or default directories. |
| service reset | Resets service startup information, creating default links as specified in the chkconfig entry in the service's init.d startup script. |

The off option configures a service to shut down if the system enters a specified runlevel. The next example shuts down the Web server if runlevel 3 is entered. If the service is not running, it remains shut down:

```
chkconfig --level 3 httpd off
```

The reset option restores a service to its chkconfig default options as specified in the service's init.d startup script:

```
chkconfig httpd reset
```

To see just the startup information for a service, you use just the service name with the --list option:

```
chkconfig --list httpd
```

```
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

### Enabling and Disabling xinetd Services with chkconfig

Unlike redhat-config-services, chkconfig can also enable or disable xinetd services. Simply enter the xinetd service with either an on or off option. The service will be started up or shut down, and the disable line in its xinetd configuration script in the /etc/xinetd.d directory will be edited accordingly. For example, to start swat, the Samba configuration server, which runs on xinetd, you simply enter:

```
chkconfig swat on
```

```
chkconfig --list swat
```

```
swat on
```

The swat configuration file for xinetd, /etc/xinetd.d/swat, will have its disable line edited to no, as shown here:

```
disable=no
```

If you want to shut down the swat server, you can use the off option. This will change the disable line in /etc/xinetd.d/swat to read "disable=yes".

```
chkconfig swat off
```

The same procedure works for other xinetd services such as the POP3 server and finger.

### Removing and Adding Services with chkconfig

If you want a service removed entirely from the entire startup and shutdown process in all runlevels, you can use the --del option. This removes all startup and shutdown links in all the runlevel directories.

```
chkconfig --del httpd
```

You can also add services to chkconfig management with the --add option. chkconfig will create startup links for the new service in the appropriate startup directories, /etc/rc.d/rcn.d. If you have previously removed all links for a service, you can restore them with the add option.

```
chkconfig --add httpd
```

### Configuring xinetd Services for Use by chkconfig

Default runlevel information should be placed in the startup scripts that are to be managed by chkconfig. Red Hat has already placed this information in the startup scripts for the services that are installed with its distribution. You can edit these scripts to change the default information if you wish. This information is entered as a line beginning with a # sign and followed by the chkconfig keyword and a colon. Then you list the default runlevels that the service should start up on, along with the start and stop priorities. The following entry lists runlevels 3 and 5 with a start priority of 85 and a stop of 15. See the section on Service Script Tags for more information:

```
# chkconfig: 35 85 15
```

So when a user turns on the httpd service with no level option specified, chkconfig will start up httpd at runlevels 3 and 5.

```
chkconfig httpd on
```
