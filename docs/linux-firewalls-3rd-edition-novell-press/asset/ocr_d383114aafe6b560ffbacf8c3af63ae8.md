Field 10 is the packet's destination address, 192.168.1.2.

Field 11 is the IP packets total length in bytes, `LEN=28`, including both the packet header and its data.

Field 12 is the TOS fields 3 service bits, plus a reserved trailing bit, `TOS=0x00`.

Field 13 is the TOS fields top 3 precedence bits, `PREC=0x00`.

Field 14 is the packets TTL field, `TTL=40`. Time to live is the maximum number of hops (that is, routers visited) remaining before the packet expires.

Field 15 is the packets datagram ID, `ID=50655`.

Field 16 is the message protocol type contained in the packet, `PROTO=UDP`. Field values include 6 (TCP), 17 (UDP), 1 (ICMP</code>, and `PROTO=<number>` for other protocol types.

Field 17 is the packets source port, 33926.

Field 18 is the packets destination port, 111.

Field 19 is length of the UDP packet, including both the header and data, `LEN=8`.

When interpreting the log message, the most interesting fields are these:

```
Jun 19 15:24:16 DROP portmap: in=eth0 SRC=192.168.1.4 DST=192.168.1.2
PROTO=UDP SPT=33926 DPT=111
```

This says that the dropped packet is a UDP packet coming in on the eth0 interface from an unprivileged port at 192.168.1.4. It was a UDP exchange targeted to this machine's (192.168.1.2) port 111, the sunrpc/portmap port. (This can be a common message because portmap historically is one of the most commonly targeted services.)

# # Checking for Open Ports

Listing your firewall rules with `iptables -L` is the main tool available for checking for open ports. Open ports are defined to be open by your `ACCEPT` rules. Beyond the `iptables -L` command, other tools such as `netstat` are helpful for finding out what ports are listening on the firewall.

`netstat` has several uses. In the next section, we'll use it to check for active ports so that we can double-check that the TCP and UDP ports in use are the ports that the firewall rules are accounting for.

Just because `netstat` reports the port as listening or open doesn't mean that its accessible through the firewall rules. Following this, two third-party port-scanning tools—`strobe` and