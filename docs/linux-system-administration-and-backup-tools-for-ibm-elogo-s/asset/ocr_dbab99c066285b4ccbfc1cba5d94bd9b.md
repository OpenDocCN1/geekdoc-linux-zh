```
# [root@test1 xinetd]# cat telnet
# default: no
# description: The telnet server serves telnet sessions; it uses \
# unencrypted username/password pairs for authentication.
service telnet
{
    flags = REUSE
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/telinetd
    log_on_failure += USERID
}
[root@test1 xinetd]# #
```

Figure 75. The /etc/xinetd.telnet file

Verify the service file in the /etc/xinetd directory. If it is not, you can create it.

Now we need to edit the /etc/hosts.allow and /etc/hosts.deny files.

In the /etc/hosts.allow file, which is shown in Figure 76, you see that the only host that is the localhost, which is 127.0.0.1. This means you can do a telnet localhost or telnet 127.0.0.1 and that is unless access is prevented by the hosts.deny file.

```
# hosts.allow This file describes the names of the hosts which are
# allowed to use the local INET services, as decided
# by the /usr/sbin/tcpd server.
# See man hosts_access(5) for more information

ALL : 127.0.0.1
```

Figure 76. The /etc/hosts.allow file

In order to add additional remote access to your server, you need to add an additional line. If you want to allow access to all other hosts then add the line:

```
ALL : ALL
```

This will enable your remote access.