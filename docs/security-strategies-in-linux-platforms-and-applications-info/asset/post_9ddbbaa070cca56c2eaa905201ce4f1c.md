
# PART 2 | Layered Security and Linux

## Basic Firewall Commands

In a typical firewall configuration file, you'll find chains of iptables commands.
The rules defined by each iptables command in a chain are considered one by one,
The basic format of the command is as follows:

```
iptables -t table option direction packet_pattern -j action
```

Now let's examine each of these options in turn.

### The iptables Table Option

The first option associated with iptables is the -t option, also known as the table
switch. Two basic options for this switch are available (the default is filter):

- * filter—Specifies rules for filtering packets.
- nat—Short for network address translation, the iptables -t nat command
can be used to configure masquerading.

For example, the following command configures masquerading on the first Ethernet
device, eth0. This presumes some other network device such as eth1 is connected
to and configured on some internal IP address network:

```
iptables -t nat -A PRERUTING -o eth0 -j MASQUERADE
```

Normally, this is followed by two other commands that allow forwarding between
the normed Ethernet network cards:

```
iptables -A FORWARD -i eth0 -o eth1 -m state
--state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

These two commands provide an introduction to the other -t switch, for packet filtering.
The -t filter option is the default, it does not need to be included in the command.
The first command takes packets from the external interface (eth0) and checks the
state of their modules (-m state). For packets where connections have been
ESTABLISHED or RELATED to an existing connection, the iptables rule jumps (-j)
to ACCEPT the packet. The second command accepts and forwards all packets from
network card eth1 destined for outside networks through network card eth0.

Of course, iptables rules can be more complex.

### Options and Directions for the iptables Command

In this section, you will examine six basic options for the iptables command. In most cases,
iptables options can be specified as letters or more expressive word switches, as:

- -A (-append)—Appends a rule to the end of a chain
- -I (--insert)—Inserts a rule in a chain of rules, as rule number n
- -R (-replace)—Replaces a rule in a chain of rules, as rule number n
- -D (-delete)—Deletes a rule in a chain of rules, as rule number n

![](img/c0608a8c8a0777903dfec4ff61fdffa1_209_0.png)

## CHAPTER 7 | Networks, Firewalls, and More

- -L (--list)—Lists existing iptables rules
- -F (--flush)—Deletes (flushes) all configured rules in the specified chain

The two commands are frequently executed on their own. For example, the iptables -L command lists all active rules defined in associated configuration files. If there is a problem, you may choose to temporarily disable the firewall with the iptables -F command. As long as any firewall configuration files still exist, you should be able to reactivate the current firewall with the following command:

```
# iptables-restore /path/to/iptables_configuration_file
```

When appropriate, these options should be coupled with a direction based on the source and destination of the packet. The three available directions are as follows:

- INPUT—Applies the iptables rule to incoming packets.
- OUTPUT—Applies the iptables rule to outgoing packets.
- FORWARD—Applies the iptables rule to incoming packets that are being sent (forwarded) to other systems.

### Packets and Patterns for the iptables Command

Once the option and direction for the iptables command is determined, the next step is the pattern match for the packet. In other words, the iptables command can be used to check for characteristics such as the IP address. For example, the following options are based on source and destination IP addresses:

- -s ip_address—The rule is applied to packets that come from the noted source address.
- d ip_address—The rule is applied to packets that are directed to the noted destination address.

Other characteristics may be associated with the protocol and TCP/IP port defined in the packet. For example, the -p switch can switch the packet type at the application layer of the TCP/IP protocol suite. The three packet-type options at this level are TCP, UDP, and the Internet Control Message Protocol (ICMP). The TCP and UDP protocols are usually associated with a port number.

### Actions for the iptables Command

The previous parts of the iptables command define a packet. Once defined, you need to tell the iptables command what to do with the packet. The four options that follow are associated with the j switch:

- -j DROP—The packet is dropped; no response is sent to the source of the network packet.
- j REJECT—Despite the name of the option, the packet is dropped; however, an error message is sent to the system that is the source of the network packet.
- -j LOG—The packet is logged: other -j switches may specify actions that may follow.
- -j ACCEPT—The packet is accepted, and is sent to the destination specified in the header of the packet.

### Sample iptables Commands

With the iptables options shown, you should be able to understand several different kinds of commands. As an example, Figure 7-1 shows an excerpt of the Red Hat /etc/sysconfig/iptables configuration file. These options are added to the iptables command during the boot process. If you are administering Red Hat systems, pay careful attention. Some of these rules may not be necessary for your configuration. In fact, many firewalls include hundreds of iptables commands. Such complexity can lead to errors. In many cases, fewer iptables rules lead to a more secure system.

> FYI While this discussion is based on a Red Hat iptables configuration file, similar guidelines apply to Ubuntu-based configuration files. One example, based on Ubuntu’s uncomplicated (ufw) package, stores comparable configuration files in the /etc/ufw/ directory. While the iptables chain used for Red Hat systems is normally named RH-Firewall-1-INPUT, that’s just a label. If you use the ufw package, you will end up with several different chains. For that reason, this section is focused on the Red Hat based firewalls.

```
:RH-Firewall-1-INPUT [0:]
-A INPUT -j RH-Firewall-1-INPUT
-A FORWARD -j RH-Firewall-1-INPUT
-A RH-Firewall-1-INPUT -p icmp --icmp-type any -j ACCEPT
-A RH-Firewall-1-INPUT -p 50 --dport 139 -j ACCEPT
-A RH-Firewall-1-INPUT -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -p udp --dport 5353 --dport 424:0:251 -j ACCEPT
-A RH-Firewall-1-INPUT -p tcp --dport 6343 -j ACCEPT
-A RH-Firewall-1-INPUT -m state ESTABLISHED,RELATED -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 2049 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 443 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -p udp --dport 137 -j ACCEPT
-A RH-Firewall-1-INPUT -m NEW -p udp --dport 138 -j ACCEPT
-A RH-Firewall-1-INPUT -m NEW -p udp --dport 137 -j ACCEPT
-A RH-Firewall-1-INPUT -m NEW -p tcp --dport 445 -j ACCEPT
-A RH-Firewall-1-INPUT -m NEW -p tcp --dport 80 -j ACCEPT
-A RH-Firewall-1-INPUT -m NEW -p udp --dport 161 -j ACCEPT
-A RH-Firewall-1-INPUT -m NEW -p udp --dport 902 -j ACCEPT
-A RH-Firewall-1-INPUT -j REJECT
COMMIT
```
