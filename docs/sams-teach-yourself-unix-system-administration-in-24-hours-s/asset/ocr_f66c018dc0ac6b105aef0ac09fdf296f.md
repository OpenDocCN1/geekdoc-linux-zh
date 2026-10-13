```
log_on_success = HOST PID
log_on_failure = HOST
cps = 25 30
}

includedir /etc/xinetd.d
```

This demonstrates the basic structure of xinetd configuration. A service is listed, then a set of parameters within curly brackets are set with name = value pairs. In this instance, the special service defaults enables certain parameters to be set for all enabled services.

The specific settings here are instances (the maximum number of concurrent connections a service is permitted), log_type (it's using syslog, with the authpriv facility—see the syslog discussion a bit earlier in this hour), and on successful connections, it logs HOST and PID, while on failures it logs HOST only. Finally, there's a fail-safe connections-per-second parameter that specifies that services can accept a maximum of 25 connections per second, and if the rate exceeds this value, the service will be shut down completely for 30 seconds.

The last line is the most important: It indicates that the remainder of the configuration information is located in individual files in the /etc/xinetd.d directory.

![](bbox=[0.27, 0.64, 0.32, 0.73])

> There are quite a few different parameters that can be specified in the xinetd.conf files. Rather than list them all here, we'll focus on the most important. For a complete list, see the xinetd.conf(5) man page.

2. To continue this exploration, we'll switch our attention to the includedir directory:

```
# cd /etc/xinetd.d
# ls -s
total 18
1 chargen      1 echo        1 rexec       1 sgi_fam      1 time-udp
1 chargen-udp  1 echo-udp    1 rlogin      1 talk         1 wu-ftpd
1 daytime      1 finger      1 rsh         1 telnet
1 daytime-udp  1 ntalk       1 rsync       1 time
```

There are seemingly quite a few services enabled with xinetd, but further examination of a specific configuration file—in this case telnet—shows that it's not quite as bad as it seems:

```
# cat telnet
# default: on
# description: The telnet server serves telnet sessions; it uses
# unencrypted username/password pairs for authentication.
## CHANGED TO DISABLE TELNET 12/2001
```