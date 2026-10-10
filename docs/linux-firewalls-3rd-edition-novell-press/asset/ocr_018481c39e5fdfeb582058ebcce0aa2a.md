```
IPT -A INPUT -i $INTERNET -p tcp \
--sport SUNPRIVPORTS \
-d $IPADDR --dport 113 -j ACCEPT
```

```
IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 113 \
--dport SUNPRIVPORTS -j ACCEPT
```

If you decide not to offer the service, it’s a good practice to reject the connection request to avoid waiting for the TCP connection timeout. This is the case only when an incoming packet is rejected rather than dropped, in these examples:

```
IPT -A INPUT -i $INTERNET -p tcp \
--sport SUNPRIVPORTS \
-d $IPADDR --dport 113 -j REJECT --reject-with tcp-reset
```

Alternatively, you could use the accept rules but not run the `identd` server. The result would be the same: The TCP layer would return a TCP RST message to the sender.

# Enabling Common TCP Services

It’s likely that no one will want to enable all the services listed in this section, but most everyone will want to enable some subset of them. These are the services most often used over the Internet today. As such, this section is more of a reference section than anything else. This section provides rules for the following:

+   - Email
+   - Usenet
+   - Telnet
+   - SSH
+   - FTP
+   - Web services
+   - Whois
+   - RealAudio, RealVideo, and QuickTime

Many other services are available that aren’t covered here. Some of them are used on specialized servers, some are used by large businesses and organizations, and some are designed for use in local, private networks. Additional LAN and DMZ services are covered in Chapter 6.