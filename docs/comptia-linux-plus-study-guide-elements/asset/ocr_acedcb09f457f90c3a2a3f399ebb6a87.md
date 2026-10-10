A complete chain is created by issuing multiple `iptables` commands, each of which defines a single rule. You can then view the result by typing `iptables -L`, as described earlier.

# A Sample `iptables` Configuration

Because `iptables` creates a complete firewall configuration only through the use of multiple calls to the utility, Linux packet-filter firewalls are frequently created via shell scripts that repeatedly call `iptables`. (Chapter 2, "Using Text-Mode Commands," introduces shell scripts, so review it if you need more information on the basics of creating a script.) These scripts may be called as SysV startup scripts or in some other way as part of the startup procedure. For learning purposes, you may want to create a script that's not called in this way, though. Listing 9.1 shows a sample script that demonstrates the key points of firewall creation.

# Listing 9.1: Sample Linux Firewall Script

```
```bash
#!/bin/bash

iptables -F INPUT
iptables -F FORWARD
iptables -F OUTPUT

iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

# Let traffic on the loopback interface pass
iptables -A OUTPUT -d 127.0.0.1 -o lo -j ACCEPT
iptables -A INPUT -s 127.0.0.1 -i lo -j ACCEPT

# Let DNS traffic pass
iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
iptables -A INPUT -p udp --sport 53 -j ACCEPT

# Let clients' TCP traffic pass
iptables -A OUTPUT -p tcp --dport 1024:65535 -m state \
	--state NEW,ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 1024:65535 -m state \
	--state ESTABLISHED,RELATED -j ACCEPT

# Let local connections to local SSH server pass
iptables -A OUTPUT -p tcp --sport 22 -d 172.24.1.0/24 -m state \
	--state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -s 172.24.1.0/24 -m state \
	--state NEW,ESTABLISHED,RELATED -j ACCEPT
```
```