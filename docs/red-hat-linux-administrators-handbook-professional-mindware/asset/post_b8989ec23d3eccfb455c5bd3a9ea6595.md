
of them, simply edit the appropriate service file in the `/etc/xinetd.d` directory and add a line as follows:

```
disable = yes
```

This line will disable the appropriate service run by xinetd. However, before xinetd knows about this change, you must reload the xinetd configuration file by running the following command:

```
killall USR1 xinetd
```

If you wish to never run an Internet service, you might want to completely remove the appropriate service file from `/etc/xinetd.d` directory and reload the xinetd configuration file as mentioned above. This way you are sure that the service is disabled forever.

On the other hand, if you wish to not disable a service completely but partially make it available to a restricted set of IP addresses or networks, you can add:

```
only_from <IP address or network>
```

within a service definition file to control access.

## Using the TCP wrapper program to secure xinetd run services

The TCP wrapper program can control access to xinetd run services. Any xinetd run service can be run via a TCP wrapper by modifying the appropriate service file in the `/etc/xinetd.d` directory. The lines that need to be added or modified are the following:

```
flags             = REUSE NAMEINARGS
server            = /usr/sbin/tcpd
server_args       = /path/to/service_daemon
```

The `server_args` line needs to be set to the path of the service daemon. For example, to run the FTP service via the TCP wrapper, the `/etc/xinetd.d/wu-ftpd` service definition file might look like:

```
service ftp
{
       flags             = REUSE NAMEINARGS
       socket_type       = stream
       wait              = no
       user              = root
       server            = /usr/sbin/tcpd
       server_args       = /usr/sbin/in.ftpd
       log_on_success    += DURATION USERID
       log_on_failure    += USERID
       nice              = 10
}
```

The TCP wrapper program enhances security by providing the following services:

- **Logging service** can log information about a request using the syslog facility.
- **Host-based access control** can provide host-based access control using pattern matching.
- **Host name and address verification service** can detect spoofing of host names or addresses when a host is pretending to be some other host.

You can guess how important the TCP wrapper is, as it comes as part of the default Red Hat Linux installation. There is absolutely no reason for not wrapping each of your xinetd services with the TCP wrapper.

## Restricting host access via the TCP wrapper

The TCP wrapper provides a great deal of flexibility in controlling access at an Internet host (or IP address) level. This flexibility can come in very handy for configuring a tight server system. Here I discuss an example of a tightly controlled system based on a system I use daily.

First, decide on the goal of the sample control configuration. Say that you want to create an Internet Web server system that allows only Telnet, FTP, POP3, and HTTP services. Because the Web service (HTTP) is typically a high-demand service, it is not run via xinetd. Let's assume that the Web server is Apache and it is run as a stand-alone service. In this example, then, xinetd manages the rest of the services. Also, let's assume that we want to restrict Telnet, FTP, and POP3 access to only a single network whose network address is 206.171.50.0.

Listing 15-3 shows the flags, server, and server argument lines for each of these services.

### Listing 15-3 Flags, server, and server_args lines for Telnet, FTP, and POP3

```
# Telnet (in /etc/xinetd.d/telnet)

    flags       = REUSE NAMEINARGS
    server      = /usr/sbin/tcpd
    server_args = /usr/sbin/in.telnetd

# FTP (in /etc/xinetd.d/wu-ftpd)

    flags       = REUSE NAMEINARGS
    server      = /usr/sbin/tcpd
    server_args = /usr/sbin/in.ftpd

# POP3 (in /etc/xinetd.d/ipop3)

    flags       = REUSE NAMEINARGS
    server      = /usr/sbin/tcpd
    server_args = /usr/sbin/in.ipop3d
```

Now you need to restrict access to these services via the `/etc/hosts.allow` and `/etc/hosts.deny` files. The `/etc/hosts.allow` file is used to specify which hosts are allowed access to a xinetd service, and the `/etc/hosts.deny` file is used to specify which hosts are not allowed access to a xinetd service. Both of these files use the same configuration format as shown here:

```
daemon list : client list [ : shell command ]
```

The daemon list is a list of one or more service process names. For instance, `in.ftpd`, `in.telnetd`, and `ipop3d` are daemon names for this example. The client list consists of one or more host names or IP addresses. You can use the wildcards shown in Table 15-6 in both daemon and client lists.

### Table 15-6 Wildcards for Daemon and Client Lists in /etc/hosts.{allow | deny} Files

| Wildcard | Meaning |
| :--- | :--- |
| ALL | Always matches. |
| LOCAL | Matches a local host name such as wormhole, but not wormhole.nitec.com. |
| UNKNOWN | Matches when the host name or IP address is unknown because of a problem. |
| KNOWN | Matches when a host or IP address is known. |
| PARANOID | Matches a host that does not match its IP address. This works only if the TCP wrapper program was not built with the -DPARANOID option at compilation. |

You can also use patterns such as the following:

1. `nitec.com` matches a host name such as wormhole.nitec.com or pisco.nitec.com. In other words, when a leading dot is used in a pattern, it can be matched from the right side of the host name.
2. `206.171.50.*` matches any hosts with addresses in the range of 206.171.50.0 to 206.171.50.255. In other words, when a trailing dot is used in a pattern, the matching is done from the left.
3. `206.171.50.0/255.255.255.0` matches any hosts with addresses in the range of 206.171.50.0 to 206.171.50.255. The pattern is treated as a network/netmask definition.

Also, if you plan to use shell commands to perform some action, take advantage of the character expansions shown in Table 15-7.

### Table 15-7 Character Expansions for Shell Commands

| Character | Expanded Meaning |
| --- | --- |
| $a | The IP address of the client trying to access a service |
| $A | The IP address of the server |
| $c | Client information such as host name or IP address, or user@host or user@ip_address, etc. |
| $d | The name of the daemon or service |
| $h | The host name of the client trying to access a service |
| $H | The host name of the server |
| $p | The process ID (PID) of the daemon or service |
| $s | Server information such as host name or IP address, or user@host or user@ip_address, etc. |
| $u | The client username, if known; or else set to unknown |
| $% | The % character |

Because the goal in this example is to disallow all the hosts except for the ones belonging to the 206.171.50.0 network, you can create a `/etc/hosts.deny` file, as shown in Listing 15-4.

### Listing 15-4 The /etc/hosts.deny file

```
# hosts.deny   This file describes the names of the
# hosts that are not allowed to use the local INET
# services, as decided by the /usr/sbin/tcpd program.
#

# Deny all daemon access to all hosts.
#
ALL : ALL
```

The `/etc/hosts.deny` file is set up to deny all hosts. The single configuration line `ALL : ALL` tells the TCP wrapper (tcpd) to deny all daemon access to all hosts. If it is left as is and no `/etc/hosts.allow` file exists in the system, no host will be able to access any of the three xinetd-run services (Telnet, FTP, and POP3). So, you must allow specific hosts, particularly the 206.171.50.0 network, to access these services in the `/etc/hosts.allow` file. This is done in Listing 15-5.

### Listing 15-5 The /etc/hosts.allow file

```
#
#
# hosts.allow   This file describes the names of the
# hosts that are allowed to use the local INET
# services, as decided by the /usr/sbin/tcpd program.
#

# Deny all daemon access to all hosts.
#
ALL : 206.171.50.0/255.255.255.0
```

Here, the single configuration line `ALL : 206.171.50.0/255.255.255.0` states that the TCP wrapper (tcpd) should allow access to all daemons for the specified 206.171.50.0 network. In other words, all the hosts
