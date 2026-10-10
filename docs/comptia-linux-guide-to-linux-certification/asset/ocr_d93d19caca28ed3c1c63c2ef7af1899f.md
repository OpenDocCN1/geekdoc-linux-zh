service daemons are not run as the root user on the system when possible. If a hacker gains access to your system via a network service daemon run as the root user, the hacker has root access as well. Many network daemons, such as Apache, set the user account by which they execute in their configuration files.

Similarly, for daemons such as Apache that run as a non-root user, you should ensure that the shell listed in /etc/passwd for the daemon is set to an invalid shell, such as /sbin/nologin. If a hacker attempted to remotely log into the system using a well-known daemon account, she would not be able to get a BASH shell. Instead, the /sbin/nologin simply prints the warning listed in the /etc/nologin.txt file to the screen and exits. If the /etc/nologin.txt file doesn't exist, the /sbin/nologin program prints a standard warning.

In addition, because network attacks are reported in the open source community, new versions of network services usually include fixes for known network attacks. As such, these new versions are more resilient to network attacks. Because of this, it is good form to periodically check for new versions of network services, install them, and check the associated documentation for new security-related parameters that can be set in the configuration file.

If you use network services that are started by inetd or xinetd, you can use TCP wrappers to provide extra security. A **TCP wrapper** is a program (/usr/sbin/tcpd) that can start a network daemon. To enable TCP wrappers, you must modify the /etc/inetd.conf file (for inetd) or the appropriate file in the /etc/xinetd.d directory (for xinetd) and start the network daemon as an argument to the TCP wrapper. For the telnet daemon started by xinetd, you modify the /etc/xinetd/telnet file, as shown in the following example:

```
```
[root@server1 ~]# cat /etc/xinetd.d/telnet
# default: on
# description: the telnet server serves telnet sessions; it uses \
#   unencrypted username/password pairs for authentication.
service telnet
{
    flags            = REUSE
    socket_type      = stream
    wait             = no
    user             = root
    server           = /usr/sbin/tcpd
    server_args      = /usr/sbin/in.telnetd
    log_on_failure   += USERID
    disable          = no
}
[root@server1 ~]# _
```
```

Now, the telnet daemon (/usr/sbin/in.telnetd) will be started by the TCP wrapper (/usr/sbin/tcpd). Before a TCP wrapper starts a network daemon, it first checks the /etc/hosts.allow and /etc/hosts.deny files. This allows you to restrict the network service such that it can only be accessed by certain hosts within your organization. The following /etc/hosts.allow and /etc/hosts.deny files only give the computers client1 and client2 the ability to use the telnet utility to connect to your telnet server.

```
```
[root@server1 ~]# cat /etc/hosts.deny
in.telnetd: ALL
```
```