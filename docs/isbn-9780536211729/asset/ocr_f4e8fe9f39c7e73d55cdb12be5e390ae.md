# 7.5 Enabling Common TCP Services

```
-d IPADDR --dport 23 \\n-m state --state NEW -j ACCEPT
```

fi

```
$IPT -A INPUT -i INTERNET -p tcp \\n--sport UNPRIVORTS \\n-d IPADDR --dport 23 -j ACCEPT
```

```
$IPT -A OUTPUT -o INTERNET -p tcp ! --syn \\n-s IPADDR --sport 23 \\n--dport UNPRIVORTS -j ACCEPT
```

Rather than allowing connections from anywhere, it is far preferable to define server rules for each specific host or network that an incoming connection can legitimately originate from. SSH clients are freely available for almost all systems in use today.

# 7.5.4 SSH (TCP Port 22)

With the expiration of the RSA patent in 2000, OpenSSH, secure shell, is included in Linux distributions. It is also freely available from preferable telnet for remote login access because both ends of the connection authentication keys for both hosts, and because data is encrypted. Additionally, SSH is more than a remote login service. It can automatically direct X Window connections between remote sites, and FTP and other TCP-based connections can be directed over the more secure SSH connection. Provided that the other end of the connection allows SSH connections, it's possible to route all TCP connections through the firewall using SSH. As such, SSH is something of a poor man's virtual private network (VPN).

The ports used by SSH are highly configurable. By default, connections are initiated between a client's unprivileged port and the server's assigned service port 22. The SSH client uses the unprivileged ports exclusively. The rules in this example apply to the default SSH port:

```
SSH_PORTS="1024:65535" # RSA authentication
```

or

```
SSH_PORTS="1020:65535" # Rhost authentication
```

The client and server rules here allow access to and from anywhere. In practice, you would limit the external addresses to a select subset, particularly both ends of the connection must be configured to recognize each individual user account for authentication. Table 7.6 lists the complete client/server connection protocol for the SSH service.