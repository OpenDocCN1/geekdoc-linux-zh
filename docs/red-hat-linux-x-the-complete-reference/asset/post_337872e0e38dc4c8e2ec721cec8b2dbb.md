
## Table 19-5: iptables Options

| Option | Function |
|---|---|
| `--to-source <ipaddr>[ - <ipaddr> ][:port-port]` | Used with the SNAT target, rewrites packets with new source IP address. |
| `--to-destination <ipaddr>[ - <ipaddr> ][:port-port]` | Used with the DNAT target, rewrites packets with new destination IP address. |
| `-n` | Numeric output of addresses and ports, used with `-L`. |
| `-o [!] name[+]` | Specifies an output network interface using its name (for example, eth0). Can be used only with FORWARD and OUTPUT chains. |
| `-t table` | Specifies a table to use, as in `-t nat` for the NAT table. |
| `-v` | Verbose mode, shows rule details, used with `-L`. |
| `-x` | Expands numbers (displays exact values), used with `-L`. |
| `[!] -f` | Matches second through last fragments of a fragmented packet. |
| `[!] -V` | Prints program version. |
| `!` | Negates an option or address. |
| `-m` | Specifies a module to use, such as state. |
| `--state` | Specifies options for the state module such as NEW, INVALID, RELATED, and ESTABLISHED. Used to detect packet's state. NEW references SYN packets (new connections). |
| `--syn` | SYN packets, new connections. |
| `--tcp-flags` | TCP flags: SYN, ACK, FIN, RST, URG, PSH, and ALL for all flags. |
| `--limit` | Option for the limit module (`-m limit`). Used to control the rate of matches, matching a given number of times per second. |
| `--limit-burst` | Option for the limit module (`-m limit`). Specifies maximum burst before the limit kicks in. Used to control denial-of-service attacks. |

In the following example, the user adds a rule to the INPUT chain to accept all packets originating from the address 192.168.0.55. Any packets that are received (INPUT) whose source address (-s) matches 192.168.0.55 are accepted and passed through (-j ACCEPT).

```
iptables -A INPUT -s 192.168.0.55 -j ACCEPT
```

## Accepting and Denying Packets: DROP and ACCEPT

There are two built-in targets, DROP and ACCEPT. Other targets can be either user-defined chains or extensions added on, such as REJECT. There are two special targets used to manage chains, RETURN and QUEUE. RETURN indicates the end of a chain and returns to the chain it started from. QUEUE is used to send packets to user space.

```
iptables -A INPUT -s www.myjunk.com -j DROP
```

You can turn a rule into its inverse with an ! symbol. For example, to accept all incoming packets except those from a specific address, place an ! symbol before the -s option and that address. The following example will accept all packets except those from the IP address 192.168.0.45:

```
iptables -A INPUT -j ACCEPT ! -s 192.168.0.45
```

You can specify an individual address using its domain name or its IP number. For a range of addresses, you can use the IP number of their network and the network IP mask. The IP mask can be an IP number or simply the number of bits making up the mask. For example, all of the addresses in network 192.168.0 can be represented by 192.168.0.0/255.255.255.0 or by 192.168.0.0/24. To specify any address, you can use 0.0.0.0/0.0.0.0 or simply 0/0. By default, rules reference any address if no -s or -d specification exists. The following example accepts messages coming in that are from (source) any host in the 192.168.0.0 network and that are going (destination) anywhere at all (the -d option is left out or could be written as -d 0/0):

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

The iptables rules are usually applied to a specific network interface such as the Ethernet interface used to connect to the Internet. For a single system connected to the Internet, you will have two interfaces, one that is your Internet connection and a localhost interface (lo) for internal connections between users on your system. The network interface for the Internet is referenced using the device name for the interface. For example, an Ethernet card with the device name /dev/eth0 would be referenced by the name eth0. A modem using PPP protocols with the device name /dev/ppp0 would have the name ppp0. In iptables rules, you use the -i option to indicate the input device; it can be used only with the INPUT and FORWARD chains. The -o option indicates the output device and can be used only for OUTPUT and FORWARD chains. Rules can then be applied to packets arriving and leaving on particular network devices. In the following examples, the first rule references the Ethernet device eth0, and the second, the localhost:

```
iptables -A INPUT -j DROP -i eth0 -s 192.168.0.45
iptables -A INPUT -j ACCEPT -i lo
```

## User-Defined Chains

With iptables, the FORWARD and INPUT chains are evaluated separately. One does not feed into the other. This means that if you want to completely block certain addresses from passing through your system, you will need to add both a FORWARD rule and an INPUT rule for them.

```
iptables -A INPUT -j DROP -i eth0 -s 192.168.0.45
iptables -A FORWARD -j DROP -i eth0 -s 192.168.0.45
```

A common method for reducing repeated INPUT and FORWARD rules is to create a user chain that both the INPUT and FORWARD chains feed into. You define a user chain with the -N option. The next example shows the basic format for this arrangement. A new chain is created called incoming (it can be any name you choose). The rules you would define for your FORWARD and INPUT chains are now defined for the incoming chain. The INPUT and FORWARD chains then use the incoming chain as a target, jumping directly to it and using its rules to process any packets they receive.

```
iptables -N incoming
iptables -A incoming -j DROP -i eth0 -s 192.168.0.45
iptables -A incoming -j ACCEPT -i lo
iptables -A FORWARD -j incoming
iptables -A INPUT -j incoming
```

## ICMP Packets

Firewalls often block certain Internet Control Message Protocol (ICMP) messages. ICMP redirect messages, in particular, can take control of your routing tasks. You need to enable some ICMP messages, however, such as those needed for ping, traceroute, and particularly destination-unreachable operations. In most cases, you always need to make sure destination-unreachable packets are allowed; otherwise, domain name queries could hang. Some of the more common ICMP packet types are listed in Table 19-6. You can enable an ICMP type of packet with the --icmp-type option, which takes as its argument a number or a name representing the message. The following examples enable the use of echo-reply, echo-request, and destination-unreachable messages, which have the numbers 0, 8, and 3.

```
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type echo-reply -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type echo-request -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type destination-unreachable -d 10.0.0.1
```

Their rule listing will look like this:

```
ACCEPT icmp -- 0.0.0.0/0 10.0.0.1 icmp type 0
ACCEPT icmp -- 0.0.0.0/0 10.0.0.1 icmp type 8
ACCEPT icmp -- 0.0.0.0/0 10.0.0.1 icmp type 3
```

Ping operations need to be further controlled to avoid the ping-of-death security threat. You can do this several ways. One way is to deny any ping fragments. Ping packets are normally very small. You can block ping-of-death attacks by denying any ICMP packet that is a fragment. Use the -f option to indicate fragments.

```
iptables -A INPUT -p icmp -j DROP -f
```

Another way is to limit the number of matches received for ping packets. You use the limit module to control the number of matches on the ICMP ping operation. Use -m limit to use the limit module, and --limit to specify the number of allowed matches. 1/s will allow one match per second.

```
iptables -A FORWARD -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

### Table 19-6: Common ICMP Packets

| Number | Name | Required By |
|---|---|---|
| 0 | echo-reply | ping |
| 3 | destination-unreachable | Any TCP/UDP traffic |
| 5 | redirect | Routing if not running routing daemon |
| 8 | echo-request | ping |
| 11 | time-exceeded | traceroute |

## Controlling Port Access

If your system is hosting an Internet service, such as a Web or FTP server, you can use iptables to control access to it. You can specify a particular service by using the source port (--sport) or destination port (--dport) options with the port that the service uses. iptables lets you use names for ports such as www for the Web server port. The names of services and the ports they use are listed in the /etc/services file, which maps ports to particular services. For a domain name server, the port would be domain. You can also use the port number if you want, preceding the number with a colon. The following example accepts all messages to the Web server located at 192.168.0.43:

```
iptables -A INPUT -d 192.168.0.43 --dport www -j ACCEPT
```
