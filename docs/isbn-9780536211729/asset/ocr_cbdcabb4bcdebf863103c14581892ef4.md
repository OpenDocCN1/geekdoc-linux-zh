```
$IPT -A OUTPUT -o INTERNET -p tcp ! --syn \
-s $IPADDR --sport $UNPRIVORTS \
--dport 20 -j ACCEPT
```

This unusual callback behavior, with the remote server establishing the secondary connection with your client, is part of what makes FTP difficult to secure at the packet-filter level.

# PASSIVE-MODE FTP DATA CHANNELS

The two rules allow the newer passive data channel mode used by most web browsers:

```
if [ "CONNECTION_TRACKING" = "1" ]; then \
$IPT -A OUTPUT -o INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVORTS \
--dport $UNPRIVORTS -m state --state NEW -j ACCEPT \
fi
```

```
$IPT -OUTPUT -o INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVORTS \
--dport $UNPRIVORTS -j ACCEPT

$IPT -A INPUT -i INTERNET -p tcp ! --syn \
--sport $UNPRIVORTS \
-d $IPADDR --dport $UNPRIVORTS -j ACCEPT
```

Passive mode is considered more secure than port mode because the FTP client initiates both the control and data connections, even though the connection is made between two unprivileged ports. And, as stated earlier, passive mode doesn't have the problems with NAT that port mode does on the client side.

# ALLOWING ACCESS TO YOUR LOCAL FTP SERVER

Whether to offer FTP services to the world is a difficult decision. Although FTP sites on the Internet, FTP server configuration requires great care. Numerous FTP security exploits are possible.

If your goal is to offer general read-only access to some set of files on your machine, you might consider making these files available through a web server. If your goal is to allow file uploads to your machine from the outside, FTP server access should be severely limited on the firewall level, on the inetd configuration level, or on the tcp_wrappers level, and on the FTP configuration level.

In any case, if you decide to offer FTP services, and if you decide to allow file transfers, write access should not be allowed by anonymous FTP. Remote write access to your file systems should be allowed only from specific, authenticated FTP user accounts, from specific remote sites, and to carefully controlled and limited FTP areas reserved in your file system. Hosting the FTP area from a chroot environment would be even better.