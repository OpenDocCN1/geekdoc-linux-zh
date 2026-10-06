# CHAPTER 13 Linux Firewall (Netfilter)

network (eth1) and the Internet (eth0). Note that by “server,” we are referring to anything that needs a connection to it. This could, for example, mean a Linux system running an ssh daemon or a Windows system running a web server.

First we need to make sure that the NAT module is loaded and FTP support for NAT is loaded. We do that with the modprobe commands:

```
[root@server ~]# modprobe iptables_nat
[root@server ~]# modprobe ip_nat_ftp
```

With the necessary modules loaded, we define the default policies for all chains. For the INPUT, FORWARD, and OUTPUT chains in the filter table, we set the destination to DROP, DROP, and ACCEPT, respectively. For POSTROUTING and PREROUTING chains, we set their default policies to ACCEPT. This is necessary for NAT to work.

```
[root@server ~]# iptables -P INPUT DROP
[root@server ~]# iptables -P FORWARD DROP
[root@server ~]# iptables -P OUTPUT ACCEPT
[root@server ~]# iptables -t nat -P POSTROUTING ACCEPT
[root@server ~]# iptables -t nat -P PREROUTING ACCEPT
```

With the policies in place, we need to define the baseline firewall rules. What we want to accomplish is simple: Let us on the inside network (eth1) make connections to the Internet, but let the Internet connect back. To accomplish this, we define a new chain “block” that we use for grouping our state-tracking rules together. The first rule in that chain simply that any packet that is part of an established connection or is related to an established connection is allowed. The second rule states that in order for a packet to create a new connection, it cannot originate from eth0 (Internet-facing) interface. If a packet does not match either of these two rules, the firewall forces the packet to be dropped.

```
[root@server ~]# iptables -N block
[root@server ~]# iptables -A block -m state --state ESTABLISHED,RELATED -j ACCEPT
[root@server ~]# iptables -A block -m state --state NEW ! -i eth0 -j ACCEPT
[root@server ~]# iptables -A block -j DROP
```

With the blocking chain in place, we need to call it on the INPUT and FORWARD chains. We aren’t worried about the OUTPUT chain, since only packets originating from the firewall itself come from there. The INPUT and FORWARD chains, on the other hand, need to be checked. Recall that when doing NAT, the INPUT chain will not be hit, so we need to have FORWARD do the check. If a packet is destined to the firewall, we need the checks from the INPUT chain.

```
[root@server ~]# iptables -A INPUT -j block
[root@server ~]# iptables -A FORWARD -j block
```