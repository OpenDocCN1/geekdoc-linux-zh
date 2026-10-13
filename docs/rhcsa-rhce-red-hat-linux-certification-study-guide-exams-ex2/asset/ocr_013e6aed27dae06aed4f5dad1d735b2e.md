# SELF TEST ANSWERS

# The Layers of Linux Security

1. The security option that is best for a service that isn't currently required on a system is to not install that service.

# Firewalls and Network Address Translation

2. Based on the given command, any connection attempt (including packets sent with the ping command) from the 192.168.77.77 system is rejected.

3. Rules associated with iptables-based firewalls are stored in /etc/sysconfig/iptables.

4. To set up a small office while providing Internet access to a small number of users, all you need is one dedicated IP address. The other addresses can be on a private network. Masquerading makes this possible.

5. The iptables command switch that sets up masquerading is -t nat.

# The Extended Internet Super-Server

6. The configuration files for individual xinetd services are stored in the /etc/xinetd.d directory.

7. Several acceptable options are available to reread the configuration files associated with the xinetd service. The standard option is /etc/init.d/xinetd reload; the service xinetd reload command is functionally equivalent. While you could substitute restart for reload, that's an inferior answer. A "restart" kicks off any connected users.

# TCP Wrappers

8. You are using the xinetd program to start services. To limit Telnet access to clients on the 192.168.170.0 network, you'd allow access to the network in /etc/hosts.allow and deny it to all others in /etc/hosts.deny. As /usr/sbin is in the root user path, you can cite the telnetd daemon directly and add the following directive to /etc/hosts.allow:

```
telnetd : 192.168.0.170/255.255.255.0
```

Then add the following to /etc/hosts.deny:

```
telnetd : ALL
```