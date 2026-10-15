# Table 9.7 Continued

| Application | Application Protocol | Layer 4 Protocol | Port (Assigned Number) | tcpdump Logical Port Name |
|---|---|---|---|---|
| Network Management | Simple Network Management Protocol (snmp) | UDP | 161 | snmp |
|  |  | UDP | 162 (traps) | snmp-trap |
| Network Time | Network Time Protocol (ntp) | UDP | 123 | ntp |
|  |  | TCP (rarely implemented) |  |  |
| Remote Access | Telnet | TCP | 23 | telnet |
| Routing Protocol | Border Gateway Protocol | UDP | 179 | bgp |
|  |  | TCP | 179 |  |
| System Logging | syslog | UDP | 514 | syslog |
| World Wide Web | Hyper Text Transport Protocol (http) | TCP | 80 | www |
|  |  | UDP (rarely implemented) | 80 |  |

This means the aforementioned:

```
tcpdump -n -v dst 192.168.1.101 and port 53
```

can also be entered as

```
tcpdump -n -v dst 192.168.1.101 and port domain
```

And if this command is run and someone attempts to contact the web server at http://www.newriders.com/, a name resolution attempt would be printed:

```
[root@lefty /root]# tcpdump -n -v dst 192.168.1.254 and port domain
Kernel filter, protocol ALL, datagram packet socket
tcpdump: listening on all devices
10:36:31.504218 eth0 < 10.1.1.1.domain > 192.168.1.254.1026: 1552 2/12/12
www.newriders.com, CNME newriders.com., newriders.com. A 63.69.119.220 (465) (DF)
(ttl 250, id 31408)
```

In addition to this modifier, tcpdump also supports the modifiers, not and or. A very useful application of the not modifier is to not print packets that are being created through the remote access session to the Linux node. Assuming telnet, the following tcpdump will print out all packets to and from the host except telnet:

```
tcpdump host 192.168.1.254 and not port 23
```