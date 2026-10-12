If you run tcpcdump without any arguments, you get a listing of all the packets that pass through the network:

```
# /usr/sbin/tcpcdump

tcpcdump: listening on eth0
22:46:12.730048 renato.1445832987 > visionlu.nfs: 100 readlink [nfs]
22:46:12.734424 tunoloia.1012 > visionlu.800: uo2 92
22:46:12.746763 tunoloia.22 > atman.1023: P 1442999991:1423000355 (44) ack 3798274339 win 32120 <OF> [tos 0x10]
22:46:12.765084 atman.1023 > tunoloia.22: . ack 44 win 32120 <OF> [tos 0x10]
22:46:12.778100 visionlu.800 > tunoloia.1015: uo2 56
22:46:12.780084 renaro.144837013 > visionlu.nfs: 124 lookuo [nfs]
22:46:12.780153 tunoloia.22 > atman.1023: P 44:596(552) ack 1 win 32120 <OF> [tos 0x10]
```

The dump will stop when you press Ctrl+C.

As you can see, tcpcdump by default converts IP addresses to hostnames and port numbers to service names. It also attempts to interpret some packets (such as those where the line ends with lookuo [nfs], which are NFS lookups). In some cases, the number of bytes that tcpcdump looks at (68) might not be enough to fully decode the packet. In this case, you may use the -s option to increase the number (see the -s option in Table 20.5).

You don't often want to see all the packets, especially in medium to large networks. Sometimes you want to see all the packets going between two specific hosts, or even those that use a specific service. tcpcdump takes as a parameter an optional filter expression that will select only certain packets.

tcpcdump's filter expressions consist of one or more primitives joined by the keywords and, or, and not. Each primitive consists of a qualifier followed by an ID. A qualifier consists of one or more keywords, the most common of which are shown in Table 20.4. The ID specifies the value the corresponding field must have to match the filter.

### TABLE 20.4 Most Common tcpcdump Qualifiers

| Qualifier | Matches |
| :--- | :--- |
| src host | The IP address of the host from where the packet comes. |
| dst host | The IP address of the host to which the packet is going. |
| host | The IP address of the source or the destination host. |
| src port | The port the packet is coming from. |
| dst port | The port the packet is going to. |
| port | The source or the destination port. |
| tcp, udp, or icmp | The packet's protocol is the specified one. |