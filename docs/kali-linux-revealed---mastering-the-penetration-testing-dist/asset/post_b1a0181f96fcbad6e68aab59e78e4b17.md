
# Negating Conditions

Prefixing a condition with an exclamation mark negates the condition. For example, negating a condition on the -p option matches "any packet with a protocol other than the one specified." This negation can be applied to all other conditions as well.

The -s address or -s network/mask condition matches the source address of the packet. Correspondingly, -d address or -d network/mask matches the destination address.

The -i interface condition selects packets coming from the network interface. -o interface selects packets going out on a specific interface.

The --state state condition matches the state of a packet in a connection (this requires the ipt_conrack kernel module, for connection tracking). The NEW state describes a packet starting a new connection, ESTABLISHED matches packets belonging to an already existing connection, and RELATED matches packets initiating a new relation to an existing one (which is useful for the ftp-data connections in the "active" mode of the FTP protocol).

There are many available options for iptables and ip6tables and mastering them all requires a great deal of study and experience. However, one of the options you will most often use is the one to block malicious network traffic from a host or range of hosts. For example, to silently block incoming traffic from the IP address 10.0.1.5 and the 31.13.74.0/24 class C subnet:

```bash
# iptables -A INPUT -s 10.0.1.5 -j DROP
# iptables -A INPUT -s 31.13.74.0/24 -j DROP
# iptables -n -L INPUT
```

```
Chain INPUT (policy ACCEPT)
target prot opt source
DROP all 10.0.1.5 0.0.0.0/0
DROP all 31.13.74.0/24 0.0.0.0/0
```

Another commonly-used iptables command is to prevent network traffic for a specific service or port. To allow connection to SSH, HTTP, IMAP, you could run the following commands:

```bash
# iptables -A INPUT -m state --state NEW -p tcp --dport 22 -j ACCEPT
# iptables -A INPUT -m state --state NEW -p tcp --dport 80 -j ACCEPT
# iptables -A INPUT -m state --state NEW -p tcp --dport 143 -j ACCEPT
# iptables -n -L INPUT
```

```
Chain INPUT (policy ACCEPT)
target prot opt source
DROP all 10.0.1.5 0.0.0.0/0
DROP all 31.13.74.0/24 0.0.0.0/0
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:143
```

It is considered to be good hygiene to clean up old and unnecessary rules. The easiest way to delete iptables rules is to reference the rules by line number, which you can retrieve with the --lines-numbers option. Be wary though; dropping a rule will renumber all the rules appearing further in the chain.

```bash
# iptables -n L INPUT --line-numbers
Chain INPUT (POLICY ACCEPT)
num target prot source destination
1 DROP all 10.0.0.1 0.0.0.0/0
2 DROP all 31.13.74/24 0.0.0.0/0
3 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
4 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
5 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:143
# iptables -D INPUT 2
# iptables -n L INPUT --line-numbers
Chain INPUT (POLICY ACCEPT)
num target prot source destination
1 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
2 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
3 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:143
```

There are more specific conditions, depending on the generic conditions described above. For more information refer to iptables(8) and ip6tables(8).

## 7.4.3. Creating Rules

Each rule creation requires invocation of iptables or ip6tables. Typing these commands manually can be tedious, the calls are usually stored in a script so that the system is automatically configured the same way every time the machine boots. This script can be written by hand but it can also be interesting to prepare it with a high-level tool such as fwbuilder.

```bash
# apt install fwbuilder
```

The principle is simple. In the first step, describe all the elements that will be involved in the actual rules:

- The firewall itself, with its network interfaces
- The networks, with their corresponding IP ranges
- The servers
- The ports belonging to services hosted on the servers

Next, create the rules with drag-and-drop actions on the objects as shown in Figure 7.2, “Fwbuilder’s Main Window” [page 160]. A contextual menu can change the designation (negative it, for instance). Then the action needs to be chosen and configured.

As far as IPv6 is concerned, you can either create two rulesets for IPv4 and IPv6, or create only one and let fwbuilder translate the rules assigned to the objects.

## Firewall Builder - [gnurad+plarc.fwb]

# mirenboite / Policy

| Source | Destination | Service | Interface | Direction | Action | Time | Comment |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Any | polymer | udp | 3478-3479 (STUN) | Any | Both Accept | Any | |
| 2 | Any | mirenboite | udp | 5000-5501 (SIP) | Any | Both Accept | Any | |
| 3 | Any | mirenboite | udp | | Any | Both Accept | Any | |
| 4 | Any | | | | | Any | Inbound Accept | Any | |
| 5 | Any | | | | | | Any | Outbound Accept | Any | |
| 6 | Any | | | | | | Any | Outbound Accept | Any | |

(img/4d3527b185_0.png)

fwbuilder will generate a script targeting different systems including iptables for Linux, pf for FreeBSD, and pf for OpenBSD.

## 7.4.4. Installing the Rules at Boot

In order to implement the rules each time the machine boots, you will need to register the script in one directive of the /etc/network/interfaces file.

```text
iface eth0 inet static
  address 192.168.0.1
  netmask 255.255.255.0
  gateway 192.168.0.254
  up /usr/local/etc/iptables.fw
```

This example assumes that you are using ifdown. If you are using something else (like NetworkManager or systemd-networkd), then refer to their respective documentation to find ways to execute a script after the interface.

## 7.5. Monitoring and Logging

Data confidentiality and protection is an important aspect of security but it is equally important to ensure availability of services. As an administrator and security practitioner, you must ensure that everything works as expected, and it is your responsibility to detect anomalous behavior and service degradation in a timely manner. Monitoring and logging software plays a key role in this aspect of security, providing insight into what is happening on the system and to the network.

In this section, we will review some tools that can be used to monitor several aspects of Kali.

### 7.5.1. Monitoring Logs with logcheck

The logcheck program monitors files every hour by default and sends unusual log messages in emails to the administrator for further analysis.

The list of monitored files is stored in /etc/logcheck/logcheck.logfiles. The default values work fine if the /etc/rsyslog.conf file has not been completely overhauled.

logcheck can report in various levels of detail: paranoid, server, and workstation. paranoid is very verbose and should probably be restricted to specific servers as firewalls. server is the default mode and is recommended for most servers. workstation is designed for workstations and is extremely terse, filtering out more messages than the other options.

In all cases, logcheck should probably be customized to exclude some extra messages (depending on installed services), unless you really want to receive hourly batches of log emails. Since the message selection mechanism is rather complex, /usr/share/doc/logcheck-database/README.logcheck-database.gz is a required—if challenging—read.

The applied rules can be split into several types:

- those that qualify as a cracking attempt (stored in a file in the /etc/logcheck/cracking.d/ directory);
- ignored cracking attempts (/etc/logcheck/cracking.ignore.d/);
- those classifying a message as a security alert (/etc/logcheck/violations.d/);
- ignored security alerts (/etc/logcheck/violations.ignore.d/);
- finally, those applying to the remaining messages (considered as system events)
