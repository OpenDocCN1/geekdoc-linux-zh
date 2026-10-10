
Netfilter can also be used to configure a Linux computer with two or more NICs as a NAT router. To do this, you would use the **PREROUTING**, **OUTPUT**, and **POSTROUTING** chains. Consult the `iptables` manual page for more information.

In most cases, no rules exist for the `INPUT`, `FORWARD`, or `OUTPUT` chains after a Linux installation. To create rules that are used for each chain, you must use the `iptables` command. Rules can be based on the source IP address, destination IP address, protocol used (`TCP`, `UDP`, `ICMP`), or packet status. For example, to flush all previous rules from memory, specify that forwarded packets are dropped by default and that packets are only to be forwarded if they originate from the 192.168.1.0 network, you can use the following commands:

```bash
[root@server1 ~]# iptables -F
[root@server1 ~]# iptables -P FORWARD DROP
[root@server1 ~]# iptables -A FORWARD -s 192.168.1.0/24 -j ACCEPT
[root@server1 ~]# 
```

You can then verify the list of rules for each chain in memory by using the following command:

```bash
[root@server1 ~]# iptables -L
Chain INPUT (policy ACCEPT)
target   prot opt source  destination

Chain FORWARD (policy DROP)
target   prot opt source  destination
ACCEPT   all  -- 192.168.1.0/24 anywhere

Chain OUTPUT (policy ACCEPT)
target   prot opt source  destination
[root@server1 ~]# 
```

The previous firewall example uses static packet filtering rules. Most technologies today start by using a specific port and then switch to a random port above 30000. A good example of this is SSH. The first SSH packet is addressed to port 22, but the port number is changed in the return packet to a random port above 30000 for subsequent traffic. In a static filter, you would need to allow traffic for all ports above 30000 in order to use SSH.

Instead of doing this, you can use a dynamic (or stateful) packet filter rule by specifying the `-m state` option to the `iptables` command. Stateful packet filters remember traffic that was originally allowed in an existing session and adjust their rules appropriately. For example, to forward all packets from your internal interface eth1 to your external interface eth0 on your Linux router that are addressed to port 22, you could use the following command:

```bash
[root@server1 ~]# iptables -A FORWARD -i eth1 -o eth0 -m state --state NEW -dport 22 -j ACCEPT
[root@server1 ~]# 
```

Next, you can allow all subsequent packets that are part of an allowed existing session, as shown in the following output (remember that only SSH is allowed):

```bash
[root@server1 ~]# iptables -A FORWARD -i eth1 -o eth0 -m state --state ESTABLISHED,RELATED -j ACCEPT
[root@server1 ~]# 
```

| Option | Description |
| :--- | :--- |
| -s address | Specifies the source address of packets for a rule. |
| -d address | Specifies the destination address of packets for a rule. |
| -sport port# | Specifies the source port number for a rule. |
| -dport port# | Specifies the destination port number for a rule. |
| -p protocol | Specifies the protocol type for a rule. |
| -i interface | Specifies the input network interface. |
| -o interface | Specifies the output network interface. |
| -j action | Specifies the action that is taken for a rule. |
| -m match | Specifies a match parameter that should be used within the rule. The most common match used is state, which creates a stateful packet filtering firewall. |
| -A chain | Specifies the chain used. |
| -L chain | Lists rules for a certain chain. If no chain is given, all chains are listed. |
| -P policy | Specifies the default policy for a certain chain type. |
| -D number | Deletes a rule for a chain specified by additional arguments. Rules start at number 1. |
| -R number | Replaces a rule for a chain specified by additional arguments. Rules start at number 1. |
| -F chain | Removes all rules for a certain chain. If no chain is specified, it removes all rules for all chains. |

**Table 14-2 Common iptables options**

Table 14-2 provides a list of common options to the iptables command.

![](img/c27875544958897d817484d558c208c8_678_0.png)

The order in which firewall rules are defined is the order in which they are applied. Normally, firewall rules are defined to first DROP all traffic destined for the computer (the INPUT chain) and allow only specific traffic by port number.

![](img/c27875544958897d817484d558c208c8_678_1.png)

You can use the iptables command to configure firewall rules for IPv6.

![](img/c27875544958897d817484d558c208c8_678_2.png)

Because chains and rules are stored in memory, they are lost when your computer is shut down. To ensure that they are loaded on each boot on a Fedora 20 system, run the `service iptables save` command to save all current chains and rules to the `/etc/sysconfig/iptables` file. To ensure that they are loaded on each boot on an Ubuntu Server 14.04 system, simply run the `apt-get install iptables-persistent` command; during the installation of the iptables-persistent package, you will be asked if you wish to save your iptables configuration to a file loaded by a line within `/etc/network/interfaces`.

![](img/c27875544958897d817484d558c208c8_679_0.png)

Since firewall rules can quickly become complex, some Linux distributions, such as Fedora 20, implement a **firewall daemon** (firewalld) that can configure iptables with more flexibility through the use of network zones and service names. A **network zone** defines the level of trust for network connections and can be mutable (modification to its definition is allowed) or immutable (its definition cannot be changed). Table 14-3 lists common network zones used by firewalld.

The default zone used on your system is defined in `/etc/firewalld/firewalld.conf`, and custom zone configuration is stored in `/etc/firewalld/zones`. You can manage zones and firewall rules that allow or deny traffic by service or port through the use of the **firewall-cmd** command. Some common options to the firewall-cmd command are listed in Table 14-4.

To define a firewall exception for postgresql in your default (current) zone and also ensure that this exception is loaded at boot time, you could use the following commands:

```bash
[root@server1 ~]# firewall-cmd --add-service=postgresql
success
[root@server1 ~]# firewall-cmd --permanent --add-service=postgresql
success
[root@server1 ~]# 
```

You can instead define a firewall exception for traffic by port number. For example, to define a firewall exception for SSH (TCP port 22) in your default (current) zone and also ensure that this exception is loaded at boot time, you could use the following commands:

```bash
[root@server1 ~]# firewall-cmd --add-port=22/tcp
success
```

| Network Zone | Type | Description |
| :------------ | :----- | :---------------------------------------------------- |
| drop         | Immutable | Deny all incoming connections; outgoing ones are accepted. |
| block        | Immutable | Deny all incoming connections, with ICMP host-prohibited messages issued to the sender. |
| trusted      | Immutable | Allow all network connections. |
| public       | Mutable | Public areas, do not trust other computers. |
| external     | Mutable | For computers with masquerading enabled, protecting a local network. |
| dmz          | Mutable | For computers publicly accessible with restricted access. |
| work         | Mutable | For trusted work areas. |
| home         | Mutable | For trusted home network connections. |
| internal     | Mutable | For internal network, restrict incoming connections. |

**Table 14-3 Common network zones**

| Option | Description |
|:---|:---|
| --get-zones | Displays all available network zones. |
| --get-services | Displays a list of names used by firewall to identify network services. |
| --get-default-zone | Displays the default zone. |
| --set-default-zone=zone | Sets the default zone. |
| --get-active-zones | Displays the network interfaces that are active for each network zone. |
| --list-all-zones | Displays the services that are enabled (allowed) for each network zone. |
| --list-all | Displays the services that are enabled (allowed) for the current network zone. |
| --zone=zone | Displays the services that are enabled (allowed) for the specified network zone (zone). |
| --add-service=service | Enable (allow) the specified service within the current network zone. |
| --add-service=service --permanent | Ensure that the specified service is enabled (allowed) within the current network zone at boot time. |
| --add-port=port | Enable (allow) the specified port within the current network zone. |
| --add-port=port --permanent | Ensure that the specified port is enabled (allowed) within the current network zone at boot time. |
| --remove-service=service | Disable (disallow) the specified service within the current network zone. |
| --remove-service=service --permanent | Ensure that the specified service is disabled (disallowed) within the current network zone at boot time. |
| --remove-port=port | Disable (disallow) the specified port within the current network zone. |
| --remove-port=port --permanent | Ensure that the specified port is disabled (disallowed) within the current network zone at boot time. |
| --query-service=service | Returns yes if the specified service is enabled (allowed) within the current network zone, and no if it is not. |
| --query-port=port | Returns yes if the specified port is enabled (allowed) within the current network zone, and no if it is not. |

**Table 14-4 Common firewall-cmd options**

```bash
[root@server1 ~]# firewall-cmd --permanent --add-port=22/tcp
success
[root@server1 ~]# 
```

![](img/c27875544958897d817484d558c208c8_680_0.png)

> You used the `firewall-cmd` command in the hands-on projects in Chapter 13 to allow traffic destined to your Fedora Linux virtual machine by service name.

Many Linux distributions also provide a graphical firewall configuration utility that can be used to configure netfilter by service name or port. On Fedora 20, the **Firewall Configuration utility** shown in Figure 14-4 automatically creates netfilter rules based on your selections via firewalld. You can start the Firewall Configuration utility within the GNOME desktop by opening the **Activities** menu and navigating to **Show Applications, Sundry, Firewall**.
