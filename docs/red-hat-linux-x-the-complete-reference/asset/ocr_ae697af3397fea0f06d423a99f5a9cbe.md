# Listing Services with chkconfig

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

# Starting and Stopping Services with chkconfig

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