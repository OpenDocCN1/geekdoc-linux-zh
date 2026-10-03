Each option in this syntax is described in Table 13.7.

TABLE 13.7
spray Options

| Field | Description |
|---|---|
| `-c <count>` | Specifies the number of packets to send. |
| `-d <interval>` | Specifies the number of microseconds to pause between sending packets. If you don't use a delay, you might run out of buffers. |
| `-l <packet_size>` | Specifies the packet size. |
| `<hostname>` | Specifies the system to send packets to. The hostname argument can be either a name or an Internet address. |

spray is not useful as a networking benchmark because it uses unreliable connectionless transports, such as the User Datagram Protocol (UDP). spray can report a large number of packets dropped when the drops were caused by spray's sending packets faster than they could be buffered locally (before the packets got to the network medium). spray is used, however, to verify connectivity between two hosts and to test the operation of the network.

The following example illustrates the use of spray to send 100 packets to sparc14 (-c 100). Each packet is 2048 bytes (-l 2048). The packets are sent with a delay time of 20 microseconds between each burst (-d 20):

```
spray -c100 -d20 -l2048 sparc14
```

The system responds with this:

```
sending 100 packets of length 2048 to sparc14 ...
2 packets (2.000%) dropped by sparc14
567 packets/sec, 1161394 bytes/sec
```

# NETWORK MAINTENANCE

In addition to the TCP/IP set of commands, Solaris provides several network commands that the system administrator can use to check and troubleshoot the network.