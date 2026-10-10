![](bbox=[0.138, 0.11, 0.29, 0.23])

Netfilter can also be used to configure a Linux computer with two or more NICs as a NAT router. To do this, you would use the **PREROUTING**, **OUTPUT**, and **POSTROUTING** chains. Consult the `iptables` manual page for more information.

In most cases, no rules exist for the `INPUT`, `FORWARD`, or `OUTPUT` chains after a Linux installation. To create rules that are used for each chain, you must use the `iptables command`. Rules can be based on the source IP address, destination IP address, protocol used (`TCP`, `UDP`, `ICMP`), or packet status. For example, to flush all previous rules from memory, specify that forwarded packets are dropped by default and that packets are only to be forwarded if they originate from the 192.168.1.0 network, you can use the following commands:

```
```bash
[root@server1 ~]# iptables -F
[root@server1 ~]# iptables -P FORWARD DROP
[root@server1 ~]# iptables -A FORWARD -s 192.168.1.0/24 -j ACCEPT
[root@server1 ~]# __
```
```

You can then verify the list of rules for each chain in memory by using the following command:

```
```bash
[root@server1 ~]# iptables -L
Chain INPUT (policy ACCEPT)
target   prot opt source  destination

Chain INPUT (policy DROP)
target   prot opt source  destination
ACCEPT   all  -- 192.168.1.0/24 anywhere

Chain INPUT (policy ACCEPT)
target   prot opt source  destination
[root@server1 ~]# __
```
```

The previous firewall example uses static packet filtering rules. Most technologies today start by using a specific port and then switch to a random port above 30000. A good example of this is SSH. The first SSH packet is addressed to port 22, but the port number is changed in the return packet to a random port above 30000 for subsequent traffic. In a static filter, you would need to allow traffic for all ports above 30000 in order to use SSH.

Instead of doing this, you can use a dynamic (or stateful) packet filter rule by specifying the `-m state` option to the `iptables` command. Stateful packet filters remember traffic that was originally allowed in an existing session and adjust their rules appropriately. For example, to forward all packets from your internal interface eth1 to your external interface eth0 on your Linux router that are addressed to port 22, you could use the following command:

```
```bash
[root@server1 ~]# iptables -A FORWARD -i eth1 -o eth0 -m state --state NEW -dport 22 -j ACCEPT
[root@server1 ~]# __
```
```

Next, you can allow all subsequent packets that are part of an allowed existing session, as shown in the following output (remember that only SSH is allowed):

```
```bash
[root@server1 ~]# iptables -A FORWARD -i eth1 -o eth0 -m state --state ESTABLISHED,RELATED -j ACCEPT
[root@server1 ~]# __
```
```