
## Checking the Input, Output, and Forwarding Rules

| # | Pkts | Bytes | Target | Proto | Opt | In | Out | Source/Destination | Detail |
|---|---|---|---|---|---|---|---|---|---|
| 9 | 0 | 0 | ACCEPT | tcp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | | mail.lan | tcp | | sport: 1024:65535 | dport: smtp state NEW |
| 10 | 0 | 0 | ACCEPT | udp | -- | any | eth1 | timeserver.edu | \ |
| | | | | udp | | | sport: 1024:65535 | dport: ntp state NEW |
| 11 | 0 | 0 | ACCEPT | icmp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | anywhere | | | | icmp fragmentation-needed |
| 12 | 0 | 0 | ACCEPT | icmp | -- | any | eth0 | router.private.lan | \ |
| | | | | .private.lan | | | | icmp echo-request |
| 13 | 0 | 0 | ACCEPT | icmp | -- | any | eth0 | router.private.lan | \ |
| | | | | .private.lan | | | | icmp echo-reply |
| 14 | 0 | 0 | ACCEPT | icmp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | .dmz.lan | | | | icmp echo-request |
| 15 | 0 | 0 | ACCEPT | icmp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | firewall.dmz.lan | | | | icmp echo-reply |
| 16 | 0 | 0 | ACCEPT | tcp | -- | any | eth0 | router.private.lan | \ |
| | | | | jet.private.lan | | | | tcp dport:printer state NEW |
| 17 | 0 | 0 | ACCEPT | tcp | -- | any | any | anywhere | \ |
| | | | | anywhere | | | | tcp flags:RST/RST |
| 18 | 0 | 0 | LOG | all | -- | any | any | anywhere | \ |
| | | | | anywhere | | | | LOG level warning |

The default policy for the OUTPUT chain is DROP. Denied packets are simply dropped without any notification being returned to the local program. There are 18 rules on the chain:

- **Line 1** — Any packet going out the loopback interface is allowed.
- **Line 2** — Any packet that is recognized as being part of a previously ESTABLISHED connection or exchange, or a packet that is RELATED to one, is allowed.
- **Line 3** — Local DNS requests that are forwarded to the local name server in the DMZ, server to server, are allowed.
- **Line 4** — Local DNS client requests over UDP to the local name server in the DMZ are allowed.
- **Line 5** — Local DNS client requests over TCP to the local name server in the DMZ are allowed.
- **Line 6** — The local host, the LAN router, is allowed for established connections to local SSH, HTTP, HTTPS, auth, and FTP servers in the private LAN.
- **Line 7** — The local host, the choke firewall, is allowed for established connections to local SSH servers in the DMZ.
- **Line 8** — The local host, the choke firewall, is allowed for established connections to SSH, HTTP, HTTPS, auth, and FTP servers anywhere.
- **Line 9** — The local host, the choke firewall, is allowed to send mail to the mail gateway in the DMZ.
- **Line 10** — The local host, the choke firewall, is allowed to send client **ntp** time requests to a specific remote server.
- **Line 11** — The local host, the choke firewall, is allowed to send ICMP Type 3 **fragmentation-needed** messages anywhere as part of MTU size discovery.
- **Line 12** — The local host, the LAN router, is allowed to send ICMP **ping** requests to hosts in the private LAN.
- **Line 13** — The local host, the LAN router, is allowed to send ICMP **ping** responses to hosts in the private LAN.
- **Line 14** — The local host, the choke firewall, is allowed to send ICMP **ping** requests to hosts in the DMZ.
- **Line 15** — The local host, the choke firewall, is allowed to send ICMP **ping** responses to the public firewall between the DMZ and the Internet.
- **Line 16** — The local host, the LAN router, is allowed to access the networked printer in the private LAN.
- **Line 17** — The local host is allowed to send TCP RST messages anywhere.
- **Line 18** — All other outgoing packets are logged before being dropped by the default policy.

### Checking the Forwarding Rules

The forwarding rules apply to packets passing or being routed through the machine. Forwarded packets are inspected only by the rules defined for the FORWARD chain. These packets are not inspected against rules on the INPUT or OUTPUT chains. If the packet's destination address is something other than the address of the interface on which the packet arrived, the packet is inspected by the FORWARD chain. If the packet matches a FORWARD acceptance rule, the packet is sent out the appropriate interface after being inspected by any rules defined for the POSTROUTING chains.

For the purposes of illustration, the firewall rule pair shown next forwards all TCP connections from the internal network. UDP traffic is not routed. Related ICMP traffic is routed:

```bash
iptables -A FORWARD -p tcp -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -i $LAN_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
    -s $INTERNAL_LAN_ADDRESSES -m state --state NEW -j ACCEPT
```

This section is based on a representative sample of forwarding rules. The INPUT and OUTPUT rules are mostly ACCEPT rules when the default policy is DROP. Everything is denied, by default, and you explicitly define what will be accepted:

```bash
iptables -v -L FORWARD
```

```text
Chain FORWARD (policy DROP 0 packets, 0 bytes)

pkt bytes target prot opt in out source/destination

1 67 6050 ACCEPT all -- any anywhere any anywhere  \
state RELATED, ESTABLISHED

2 0 0 ACCEPT tcp -- eth1 eth0 selected.remote.host \
host1.private.lan tcp spts:1024:65535 dpts:ssh \
flags:SYN,RST,ACK,SYN state NEW

3 0 0 ACCEPT tcp -- eth0 eth1 .private.lan \
mailserver.dmz.lan multiportdports smtp,pop3 tcp spts:1024:65535 \
flags:SYN,RST,ACK,SYN state NEW

4 1 60 ACCEPT tcp -- eth0 eth1 .private.lan \
web-proxy.dmz.lan multiportdports http,https tcp spts:1024:65535 \
flags:SYN,RST,ACK,SYN state NEW

5 1 60 ACCEPT tcp -- eth0 eth1 .private.lan \
anywhere tcp spts:1024:65535 dpts:ssh \
flags:SYN,RST,ACK,SYN state NEW

6 0 0 ACCEPT tcp -- eth0 eth1 .private.lan \
news-server.net tcp spts:1024:65535 dpt:nttp \
flags:SYN,RST,ACK,SYN state NEW

7 0 0 REJECT tcp -- eth1 any anywhere \
.private.lan tcp spts:1024:65535 dpt:auth \
reject-with icmp-port-unreachable

8 0 0 ACCEPT icmp -- any any anywhere \
anywhere icmp fragmentation-needed

9 2 168 ACCEPT icmp -- eth0 eth1 .private.lan \
anywhere icmp echo-request

10 0 0 ACCEPT tcp -- any any anywhere \
anywhere tcp flags:FIN,ACK,FIN,ACK

11 0 0 ACCEPT tcp -- any any anywhere \
anywhere tcp flags:RST,RST

12 0 0 LOG all -- any any anywhere \
anywhere LOG level warning
```

The default policy for the FORWARD chain is DROP. Denied packets are simply dropped without any notification being returned to either the local or the remote program. There are 12 rules on the chain:

- **Line 1** — Any packet recognized as being part of a previously ESTABLISHED connection or exchange, or a packet that is RELATED to one, is allowed in either direction.
- **Line 2** — Incoming SSH connections from a particular remote host to host1 in the private LAN are allowed.
- **Line 3** — Outgoing client connections to the mail gateway and pop server in the DMZ are allowed.
- **Line 4** — Outgoing client connections, both HTTP and HTTPS, are allowed to the web proxy in the DMZ.
- **Line 5** — Outgoing client connections to remote SSH servers anywhere are allowed.
- **Line 6** — Outgoing client connections to a specific remote news server are allowed.
- **Line 7** — Incoming auth requests to local ident servers are rejected.
- **Line 8** — ICMP Type 3 fragmentation-needed messages are allowed in both directions as part of MTU size discovery.
- **Line 9** — Outgoing ping ICMP echo-requests are allowed to anywhere.
- **Line 10** — FIN/ACK packets are accepted in either direction.
- **Line 11** — TCP RST packets are accepted in either direction.
- **Line 12** — All other packets in either direction are logged before being dropped by the default policy.

In this case, the -v option is generally helpful to see the incoming and outgoing network interface names. eth0 is the internal interface to the .private.lan network. eth1 is the external interface to the .dmz.lan and the Internet beyond. Remember that FORWARD rules are necessary with or without NAT. Also remember that any NAT rules are defined in the nat table. These rules are defined in the default filter table.

## TESTING AN INDIVIDUAL PACKET AGAINST THE FIREWALL RULES

The rule-checking command, the -C command in ipchains, is not yet implemented in iptables.

## Interpreting the System Logs

syslogd is the service daemon that logs system events. syslogd's main system log file is /var/log/messages. Many programs use syslogd's standard logging services. Other programs, such as the Apache web server, maintain their own separate log files.

## syslog Configuration

Not all log messages are equally important—or even interesting. This is where /etc/syslog.conf comes in. The configuration file /etc/syslog.conf enables you to tailor the log output to meet your own needs.
