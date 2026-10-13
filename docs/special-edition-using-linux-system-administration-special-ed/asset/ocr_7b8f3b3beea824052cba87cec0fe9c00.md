# **DEFINE THE priv-ext CHAIN** The priv-ext chain is set up as follows:

```
```text
# ipchains -A priv-ext -j MASQ
```
```

This rule allows all connections from the internal network to the Internet using IP masquerading.

# **DEFINE THE dmz-priv CHAIN** The dmz-priv chain is set up as follows:

```
```text
# ipchains -A dmz-priv -p udp -s 192.115.144.1 domain -j ACCEPT
# ipchains -A dmz-priv -p tcp ! -y -s 192.115.144.1 domain -j ACCEPT
# ipchains -A dmz-priv -p tcp ! -y -s 192.115.144.2 smtp -j ACCEPT
# ipchains -A dmz-priv -p tcp ! -y -s 192.115.144.3 ftp -j ACCEPT
# ipchains -A dmz-priv -p tcp ! -y -s 192.115.144.3 ftp-data -j ACCEPT
# ipchains -A dmz-priv -p tcp ! -y -s 192.115.144.4 www -j ACCEPT
# ipchains -A dmz-priv -p icmp -j icmp-acc
# ipchains -A dmz-priv -j DENY
```
```

These rules allow DNS, MAIL, FTP, Web, and ping traffic from the DMZ to the internal machines.

# **DEFINE THE dmz-ext CHAIN** The dmz-ext chain is set up as follows:

```
```text
# ipchains -A dmz-ext -p udp -s 192.115.144.1 domain -j ACCEPT
# ipchains -A dmz-ext -p tcp -s 192.115.144.1 domain -j ACCEPT
# ipchains -A dmz-ext -p tcp -s 192.115.144.2 smtp -j ACCEPT
# ipchains -A dmz-ext -p tcp -s 192.115.144.3 ftp -j ACCEPT
# ipchains -A dmz-ext -p tcp -s 192.115.144.3 ftp-data -j ACCEPT
# ipchains -A dmz-ext -p tcp ! -y -s 192.115.144.4 www -j ACCEPT
# ipchains -A dmz-ext -p icmp -j icmp-err
# ipchains -A dmz-ext -j DENY -1
```
```

These rules allow DNS, MAIL, FTP, Web, and ping traffic from the DMZ to external network.

# **DEFINE THE ext-priv CHAIN** The ext-priv chain is set up as follows:

```
```text
# ipchains -A ext-priv -j REJECT
```
```

This rule allows nothing to go from the external network (Internet) into the private internal network. The internal network uses private IP addresses and there is no way to send packets from the external network to the internal network. If you need to provide access from the Internet to a particular host in the private internal network this can be done using IP Port Forwarding (IPPORTFW).

# **CREATE CHAINS FOR THE FIREWALL**

To filter packets coming into the firewall host itself you must filter on the input chain. This requires a chain for each destination interface as follows:

```
```text
# ipchains -N ext-if
# ipchains -N dmz-if
# ipchains -N priv-if
```
```