| Option | Description |
|---|---|
| --level runlevel | Specifies a runlevel to turn on, turn off, or reset a service. |
| --list service | Lists startup information for services at different runlevels. xinetd services are just on or off. With no argument, all services are listed, including xinetd services. |
| --add service | Adds a service, creating links in the default-specified runlevels (or all runlevels, if none are specified). |
| --del service | Deletes all links for the service (startup and shutdown) in all runlevel directories. |
| service on | Turns a service on, creating a service link in the specified or default runlevel directories. |
| service off | Turns a service off, creating shutdown links in specified or default directories. |
| service reset | Resets service startup information, creating default links as specified in the chkconfig entry in the service's init.d service script. |

TABLE 21-4 Options for chkconfig

# Starting and Stopping Services with chkconfig

You use the on option to have a service started at specified runlevels, and the off option to disable it. You can specify the runlevel to affect with the --level option. If no level is specified, chkconfig will use any chkconfig default information in a service's init.d service script. Red Hat and Fedora install their services with chkconfig default information already entered (if this is missing, chkconfig will use runlevels 3, 4, and 5). The following example has the Web server (httpd) started at runlevel 5:

```
chkconfig --level 5 httpd on
```

The off option configures a service to shut down if the system enters a specified runlevel. The next example shuts down the Web server if runlevel 3 is entered. If the service is not running, it remains shut down:

```
chkconfig --level 3 httpd off
```

The reset option restores a service to its chkconfig default options as specified in the service's init.d service script:

```
chkconfig httpd reset
```

To see just the startup information for a service, you use just the service name with the --list option:

```
chkconfig --list httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```