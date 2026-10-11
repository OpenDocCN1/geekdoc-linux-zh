The Internet Super Daemon is typically used to start and manage connections for smaller network daemons such as the telnet, rlogin, and FTP daemons. It is started automatically at boot time and uses the configuration file /etc/xinetd.conf. Normally, this file incorporates all of the files in the /etc/xinetd.d directory as well. Most daemons that are managed by the Internet Super Daemon are configured by files in the /etc/xinetd.d directory named after the daemons.  
For example, the telnet daemon is configured by the Internet Super Daemon via the /etc/xinetd.d/telnet file, as shown in the following output:

```
[root@server1 root]# cat /etc/xinetd.d/telnet
# default: on
# description: The telnet server serves telnet sessions; it uses \
# unencrypted username/password pairs for authentication.

service telnet
{
    flags         = REUSE
    socket_type   = stream
    wait          = no
    user          = root
    server        = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable       = yes
}

[root@server1 root]# _
```

The preceding output displays the full path to the telnet daemon (/usr/sbin/in.telnetd). In addition, the disable = yes line in the /etc/xinetd.d/telnet file indicates that the telnet daemon is currently disabled.

> **NOTE**
> 
> After a Red Hat Fedora Core 2 Linux installation, most files in the /etc/xinetd.d directory have the line disable = yes in them to prevent them from being used.
> 
> Older Linux systems use a version of the Internet Super Daemon called inetd, which uses the configuration file /etc/inetd.conf.

Large network daemons are rarely started by the Internet Super Daemon and are hence called **stand-alone daemons**. Stand-alone daemons are typically started at boot time from files in the /etc/rc/rc\*.d directories; the ntsysv utility discussed in Chapter 9, “System Initialization and X Windows,” can be used to configure most stand-alone daemons to start in various runlevels. In addition, most stand-alone daemons can be started manually from files in the /etc/init.d or /etc/rc.d/init.d directories.