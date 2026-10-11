# Firewalls and Ports

One of the main reasons why organizations have firewalls is to protect the systems, network, and server used to transfer information. You can protect the internal server and network on your system and server to ensure the communication between external and internal networks is secure. A firewall can is software or hardware which has rules to serve as a gatekeeper to a network. The firewall has access controls defined in them, enabling you to monitor the inbound traffic called outbound and ingress traffic. This is termed egress. The traffic that satisfies these rules ensures the firewall is never dropped or discarded during a hack. This is done by opening and closing ports on the firewall that allow or reject traffic.

We have looked at what ports are and how they are used and adjusted in the Linux operating system earlier in the book.

# PING

Ping is an ICMP-based application to which you and every other user in the system or server is exposed to. When you use the ping command, you can send a code 0 and type 8 packet, indicating that the packet was just an echo. Systems that receive this package will instantly respond with a type 0 code 0 packet, an echo reply. A successful ping indicates to the system that the ping was made only on a live network. This means that you are working out of a live host. When you use the ping command, you can use the Windows command prompt. The ping will send the request at least four times by default. If you use this ping in the Linux terminal, the command will continue to run until you interrupt it.

Let us look at a successful and unsuccessful ping command.

If the host being pinged is Live

```
Ping 192.168.1.1
Pinging 192.168.1.1 with 32 bytes of data:
Reply from 192.168.1.1: bytes=32 time=2ms TTL=64
Reply from 192.168.1.1: bytes=32 time=1ms TTL=64
Reply from 192.168.1.1: bytes=32 time=1ms TTL=64
Reply from 192.168.1.1: bytes=32 time<1ms TTL=64
```

If the host is unreachable

```
Ping 192.168.1.200
```