Next, unpack the source in `/usr/src` and compile and install the `ipmasqadm` tool as follows:

```
# cd /usr/src
# tar xzvf ipmasqadm-0.4.2.tar.gz
# cd ipmasqadm-0.4.2
# make
# make install
```

This will install the ipmasqadm tool in /usr/sbin, and the modules autofw.so, mfw.so, portfw.so, and user.so in /usr/lib/ipmasqadm. A manual page for ipmasqadm is also installed in /usr/man/man8.

IP port forwarding is best illustrated by an example. Consider an HTTP server in your internal masqueraded network that you want to provide direct access to from the Internet. Assume the IP address of this server is 10.0.0.10 and the IP address of the external interface firewall machine is 192.115.144.17. To enable the desired port forwarding, you must add the following commands to your firewall startup script.

```
# /usr/sbin/ipmasqadm portfw -a
# /usr/sbin/ipmasqadm portfw -a -P tcp -L 192.115.144.17 80 -R 10.0.0.10 80
```

The first command clears the port-forwarding table. The second command adds a port-forwarding entry that forward all traffic coming to port 80 of the firewall’s external interface 192.115.144.17 to port 80 of the internal host 10.0.0.10.

# TROUBLESHOOTING

Several common problems can occur when implementing a Linux-based firewall:

+   - `ipchains -L` freezes.
+   - DNS lookups fail part of the time.
+   - IP masquerading does not work.
+   - 4096 masqueraded TCP and UDP connections are insufficient.

# ipchains -L FREEZES

The command `ipchains -L` might freeze if DNS traffic is blocked because the command will attempt to convert IP addresses to domain names through DNS. By adding the `-n` flag to the command, name lookups will be suppressed.

Alternatively, you can enable traffic for UDP port 53 and TCP port 53 so that DNS traffic will be allowed.

# DNS LOOKUPS FAIL PART OF THE TIME

If you allow only UDP port 53 for DNS queries, some DNS queries might fail. This is because some replies from DNS servers will be more than 512 bytes, which causes the client to use a TCP connection on port 53 to retrieve the data. Both UDP and TCP ports 53 should allow packets through the firewall if you want to allow DNS lookups.