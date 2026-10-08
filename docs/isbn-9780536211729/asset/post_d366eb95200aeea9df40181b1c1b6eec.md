
## Table 6.4 Chain Commands on Individual Rules

| Command | Description |
| :--- | :--- |
| -A <chain> | --append <chain> | Appends a rule to the end of a chain |
| -I <chain> | --insert <chain> | Inserts a rule at the beginning of the chain |
| -R <chain> <rule number> | --replace <chain> <rule number> <rule specification> | Replaces a rule in the chain |
| -D <chain> <rule number> | --delete <chain> <rule number> | Deletes the rule at position number within a chain |

## BASIC filter TABLE MATCH OPERATIONS

The basic filter match operations supported in the default iptables filter table are listed in Table 6.5.

### Table 6.5 filter Table Rule Operations

| Option | Description |
| :--- | :--- |
| -i | --in-interface [!] [<interface>] | For incoming packets on either the INPUT or the FORWARD chains, or their user-defined subchains, specifies the interface name that the rule applies to. If no interface is specified, all interfaces are implied. |
| -o | --out-interface [!] [<interface>] | For outgoing packets on either the OUTPUT or the FORWARD chains, or their user-defined subchains, specifies the interface name that the rule applies to. If no interface is specified, all interfaces are implied. |
| -p | --protocol [!] [<protocol>] | Specifies the IP protocol that the rule applies to. The built-in protocols are tcp, udp, icmp, and all. The protocol value can be either the name or the numeric value, as listed in /etc/protocols. |
| -s | --source \| --src [!] <address>[/<mask>] | Specifies the host or network source address in the IP header. |
| -d | --destination \| --dst [!] <address>[/<mask>] | Specifies the host or network destination address in the IP header. |
| -j | --jump <target> | Specifies the target disposition for the packet if it matches the rule. The default targets include the built-in targets, an extension, or a user-defined chain. |
| [-!] -f | --fragment | Specifies second and additional fragmented packets. The negated version of this specifies unfragmented packets. |
| -c | --set-counters <packets> <bytes> | Initializes the packet and byte counters. |

### RULE TARGETS ARE OPTIONAL

If the packet matches a rule that doesn't have a target disposition, the packet counters are updated, but list traversal continues.

## tcp filter TABLE MATCH OPERATIONS

TCP header match options are listed in Table 6.6.

### Table 6.6 tcp filter Table Match Operations

| Option | Description |
| :--- | :--- |
| -p tcp Option | This command specifies the source ports |
| --source-port \| --sport [!] <port>[:<port>] | This command specifies the destination ports |
| --destination-port \| --dport [!] <port>[:<port>] | This command tests the bits in the mask list, out of which the bits must be set in order to match |
| --tcp-flags [!] <mask>,<mask> <set>,<set> | The SYN flag must be set as an initial connection request |
| [-!] -syn | |
| --tcp-option [!] <number> | The only legal tcp option is the maximum packet size that the sending host is willing to accept. |

## udp filter TABLE MATCH OPERATIONS

UDP header match options are listed in Table 6.7.

### Table 6.7 udp filter Table Match Operations

| Option | Description |
| :--- | :--- |
| -p udp Option | Specifies the source ports |
| --source-port \| --sport [!] <port>[:<port>] | Specifies the source ports |
| --destination-port \| --dport [!] <port>[:<port>] | Specifies the destination ports |

## icmp filter TABLE MATCH OPERATIONS

ICMP header match options are listed in Table 6.8.

### Table 6.8 icmp filter Table Match Operations

| Match | Description |
| :--- | :--- |
| --icmp-type [!] <type> | Specifies the ICMP type name or number. The ICMP type is used in place of a source port. |

The major supported ICMP type names and numeric values are the following:

- echo-reply (0)
- destination-unreachable (3)
    - network-unreachable
    - host-unreachable
    - protocol-unreachable
    - port-unreachable
    - fragmentation-needed
    - network-unknown
    - host-unknown
    - network-prohibited
    - host-prohibited
- source-quench (4)
- redirect (5)
- echo-request (8)
- time-exceeded (10)
- parameter-problem (11)

## ADDITIONAL ICMP SUPPORT

iptables supports a number of additional, less common or router-specific ICMP message types and subtypes. To see the entire list, use the following iptables help command:

```bash
iptables -p icmp -h
```

## 6.4.2 filter Table Target Extensions

The filter table target extensions include logging functionality and the capability to reject a packet rather than dropping it.

Table 6.9 lists the options available to the LOG target. Table 6.10 lists the single option available to the REJECT target.

### Table 6.9 LOG Target Extension

| Option | Description |
| :--- | :--- |
| -j LOG Option | |
| --log-level <syslog level> | Log level is either the numeric or the symbolic login priority, as listed in /usr/include/sys/syslog.h. These are the same log levels used in /etc/syslog.conf. The levels are emerg (0), alert (1), crit (2), err (3), warn (4), notice (5), info (6), and debug (7). |
| --log-prefix <descriptive string> | The prefix is a quoted string that will be printed at the start of the log message for the rule. |
| --log-ip-options | This command includes any IP header options in the log output. |
| --log-tcp-sequence | This command includes the TCP packet's sequence in the log output. |
| --log-tcp-option | This command includes any TCP header options in the log output. |

### Table 6.10 REJECT Target Extension

| Option | Description |
| :--- | :--- |
| -j REJECT Option | |
| --reject with <ICMP type 3> | By default, a rejected packet results in an ICMP type 3 icmp-port-unreachable message returned to the sender. Other type 3 error messages can be returned instead, including icmp-net-unreachable, icmp-host-unreachable, icmp-proto-unreachable, icmp-net-prohibited, and icmp-host-prohibited. |
| --reject-with tcp-reset | Incoming TCP packets continue with the more standard TCP RST message, rather than an ICMP error message. |
| --reject-with echo-reply | ping echo-request messages are rejected with a failed echo-reply message. That is, the firewall generates a reply, but the request is not forwarded to the target host. |

## ULOG TABLE TARGET EXTENSION

Related to the LOG target is the ULOG target, which sends the log message to a userspace program for logging. Behind the scenes for ULOG, the packet gets multicast by the kernel through a netlink socket of your choosing (the default is socket 1). The userspace daemon would then read the message from the socket and do with it as it pleases. The ULOG target is typically used to provide more extensive logging than is possible with the standard LOG target.

As with the LOG target, processing continues after matches on a ULOG targeted rule. The ULOG target has four configuration options, as described in Table 6.11.

### Table 6.11 ULOG Target Extension

| Option | Description |
| :--- | :--- |
| --ulog-ngroup <group> | Defines the netlink group that will receive the packet. The default group is 1. |
| --ulog-prefix <prefix> | Messages will be prefixed by this value, up to 32 characters in length. |
| --ulog-crange <size> | The size in bytes to send to the netlink socket. The default is 0, which sends the entire packet. |
| --ulog-qthreshold <size> | The size in packets to queue within the kernel. The default is 1, which means that one packet is sent per message to the netlink socket. |

## 6.4.3 filter Table Match Extensions

The filter table match extensions provide access to the fields in the TCP, UDP, and ICMP headers, as well as the match features available in iptables, such as maintaining connection state, port lists, access to the hardware MAC address, and access to the IP TOS field.

## MATCH SYNTAX

The match examples require the -m or --match command to load the module, followed by any relevant match options.

## multiport filter TABLE MATCH EXTENSION

multiport port lists can include up to 15 ports per list. Whitespace isn't allowed. There can be no blank spaces between the commas and the port values. Port ranges cannot be interspersed in the list. Also, the -m multiport command must exactly follow the -p <protocol> specifier.

Table 6.12 lists the options available to the multiport match extension.

### Table 6.12 multiport Match Extension

| Option | Description |
| :--- | :--- |
| -m multiport | --match multiport |
| --source-port <port> [,<port>...] | Specifies the source port(s). |
| --destination-port <port> [,<port>...] | Specifies the destination port(s). |
| --ports <port> [,<port>...] | Source and destination ports are equal, and they match a port in the list. |

The multiport syntax can be a bit tricky. Some examples and cautions are included here. The following rule blocks incoming packets arriving on interface eth0 destined for the UDP ports associated with NetBIOS and SMB, common ports that are exploited on Microsoft Windows computers and targets for:

```bash
iptables -A INPUT -i eth0 -p udp -m multiport --destination-port 135,136,137,138,139 -j DROP
```

The next rule blocks outgoing connection requests sent through the eth0 interface to high ports using the TCP services NFS, socks, and squid:

```bash
iptables -A OUTPUT -o eth0 -p tcp -m multiport --destination-port 2049,1080,3128 --syn -j REJECT
```

What is important to note in this example is that the multiport command must exactly follow the protocol specification. A syntax error would have resulted if the --syn were placed between the -p tcp and the -m multiport.

To show a similar example of the --syn placement, the following is correct:

```bash
iptables -A INPUT -i <interface> -p tcp -m multiport --source-port 80,443 ! --syn -j ACCEPT
```
