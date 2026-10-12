Because the goal in this example is to disallow all the hosts except for the ones belonging to the 206.171.50.0 network, you can create a /etc/hosts.deny file, as shown in Listing 15-4.

# **Listing 15-4** _The /etc/hosts.deny file_

```
# hosts.deny   This file describes the names of the
# hosts that are not allowed to use the local INET
# services, as decided by the /usr/sbin/tcpd program.
#

# Deny all daemon access to all hosts.
#
ALL : ALL
```

The /etc/hosts.deny file is set up to deny all hosts. The single configuration line ALL : ALL tells the TCP wrapper (tcpd) to deny all daemon access to all hosts. If it is left as is and no /etc/hosts.allow file exists in the system, no host will be able to access any of the three inetd-run services (Telnet, FTP, and POP3). So, you must allow specific hosts, particularly the 206.171.50.0 network, to access these services in the /etc/hosts.allow file. This is done in Listing 15-5.

# **Listing 15-5** _The /etc/hosts.allow file_

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

Here, the single configuration line ALL : 206.171.50.0/255.255.0 states that the TCP wrapper (tcpd) should allow access to all daemons for the specified 206.171.50.0 network. In other words, all the hosts