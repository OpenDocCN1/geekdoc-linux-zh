Comment lines begin with the pound sign (#). The `defaults` block of attributes, enclosed in curly braces ({...}), specifies default values for some attributes. These default values apply to all other services in the configuration file. The `instances` attribute is set to 60, which means, at most, 60 servers can be simultaneously active for any service.

![](bbox=[0.13, 0.22, 0.22, 0.34])

The last line in the `/etc/xinetd.conf` file uses the `includedir` directive to include all files inside the `/etc/xinetd.d` directory, excluding files that begin with a period (.). The idea is that the `/etc/xinetd.d` directory contains all service-configuration files — one file for each type of service the `xinetd` server is expected to manage.

Here is the listing of files that appears when I type the `ls /etc/xinetd.d` command on a typical Fedora Core system (the exact content of the `/etc/xinetd.d` directory depend on the Internet services installed on your system):

```
```
chargen cups-lpd daytime-udp echo-udp ktalk services telnet time-udp
chargen-udp daytime echo finger rshcmd sgi-fam time
```
```

Each of these files specifies the attributes for one service. For example, the following listing shows the contents of the `/etc/xinetd.d/telnet` file, which specifies the `xinetd` configuration for the TELNET service:

```
```
# description: The Telnet server serves Telnet sessions; it uses
# unencrypted username/password pairs for authentication.
{
        service	telnet
        flags	= REUSE
        socket_type	= stream
        wait	= no
        user	= root
        server	= /usr/sbin/in.telnetd
        log_on_failure	+= USERID
        disable	= yes
}
```
```

The filename (in this case, `telnet`) can be anything; what matters is the service name that appears next to the `service` keyword in the file. In this case, the line `service telnet` tells `xinetd` the name of the service. `xinetd` uses this name to look up the port number from the `/etc/services` file. To look for `telnet` in the `/etc/services` file, type the following command:

```
```
grep "^telnet" /etc/services
```
```

The command displays the following lines:

```
```
telnet		23/tcp
telnet		23/udp
telnets		992/tcp
telnets		992/udp
```
```