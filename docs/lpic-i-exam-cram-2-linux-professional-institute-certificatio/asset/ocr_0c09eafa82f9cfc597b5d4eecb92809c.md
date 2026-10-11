The file contains a few lines that set the default limitations for the services governed by xinetd. If an individual service has a conflicting setting in its configuration file, that individual file setting takes precedence.

> > **ALERT** You're likely to see questions about how to have a service run as a different user, which is accomplished by editing the service's configuration file and changing the user line.

Several of these lines bear defining:

+   - **instances**—This sets the total number of daemon instances allowed; this daemon is limited to 60 instances.

+   - **cps**—This limits the number of connections per second allowed through xinetd. Any more than the maximum (25) causes the service to be disabled for 30 seconds and then check whether it can accept more connections.

+   - The other settings are log related, logging the host and PID for successful connections and just the host for unsuccessful connections

An individual service configuration file from the /etc/xinetd.d directory such as telnet would contain

```
```
 service telnet
 {
     disable     = yes
     flags       = REUSE
     socket_type = stream
     wait        = no
     user        = root
     server      = /usr/sbin/in.telnetd
     log_on_failure	+= USERID
     access_times	= 08:00-17:00
     only_from   = snowlower
 }
```
```

These files contain a number of settings:

+   - **service**—This keyword must be followed by the service name, such as telnet.

+   - **disable**—Values include *yes* (which disables the service and no connections are accepted) and *no* (which doesn't disable or enables the service for connections).

+   - **flags**—Many and varied flags exist; the most common is *REUSE*, which allows the port and service to accept multiple connections.