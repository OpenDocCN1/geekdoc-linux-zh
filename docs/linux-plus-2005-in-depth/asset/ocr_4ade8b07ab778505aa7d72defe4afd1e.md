netfilter/iptables INPUT chain rules to allow only desired network traffic to reach your network services. It is also important to ensure that network service daemons are not run as the root user on the system when possible. If a cracker gains access to your system via a network service daemon run as the root user, the cracker has root access as well. Many network daemons, such as Apache, set the user account by which they execute in their configuration files.

In addition, because network attacks are reported in the open source community, new versions of network services usually include fixes for known network attacks. As such, these new versions are more resilient to network attacks. Because of this, it is good form to periodically check for new versions of network services, install them, and check the associated documentation for new security-related parameters that can be set in the configuration file.

If you use network services that are started by the Internet Super Daemon, you can use TCP wrappers to provide extra security. A **TCP wrapper** is a program (/usr/sbin/tcpd) that can start a network service. To enable TCP wrappers, you must modify the appropriate file in the /etc/xinetd.d directory and start the network daemon as an argument to the TCP wrapper. For the telnet daemon, you modify the /etc/xinetd.d/telnet file, as shown in the following example:

```
[root@server1 root]# cat /etc/xinetd.d/telnet
# default: on
# description: The telnet server serves telnet sessions; it uses \n#
uncrypted username/password pairs for authentication.

service telnet
{

flags            = REUSE
    socket_type    = stream
    wait           = no
    user           = root
    server         = /usr/sbin/tcpd
    server_args    = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable        = yes
}
[root@server1 root]# _
```

Now, the telnet daemon (/usr/sbin/in.telnetd) will be started by the TCP wrapper (/usr/sbin/tcpd). Before a TCP wrapper starts a network daemon, it first checks the /etc/hosts.allow and /etc/hosts.deny files. This allows you to restrict the network service such that it can only be accessed by certain hosts within your organization. The following /etc/hosts.allow and /etc/hosts.deny files only allow the computers client1 and client2 the ability to use the telnet utility to connect to your telnet server.

```
[root@server1 root]# cat /etc/hosts.deny
in.telnetd: ALL
[root@server1 root]# _
```