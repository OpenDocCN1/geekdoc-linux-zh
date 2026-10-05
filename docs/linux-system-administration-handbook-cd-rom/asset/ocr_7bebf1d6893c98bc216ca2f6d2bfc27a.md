# 317 IP MASQUERADING

```
s10 Link encap:Serial Line IP
inet addr:111.222.333.444 P-t-P:555.666.777.888
Mask:255.255.255.0
UP POINTPOINT RUNNING MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:2 errors:0 dropped:0 overruns:0
```

```
ppp0 Link encap:Point-Point Protocol
inet addr:111.222.333.444 P-t-P:555.666.777.888
Mask:255.255.255.0
UP POINTPOINT RUNNING MTU:1500 Metric:1
RX packets:5 errors:0 dropped:0 overruns:0
TX packets:5 errors:0 dropped:0 overruns:0
```

# 23.5 IP MASQUERADING

Most of the options suggested in this chapter haven't needed specific version of the kernel. In order to do IP masquerading, it will require at least version 2.0 of the Linux kernel along with version 2.3.0 of ipfwadm. Actually, the kernel supports IP masquerading in the 1.2.x kernels, but ipfwadm didn't support it at that time.

Also, note that currently all forms of network traffic are not supported. Common forms of traffic, such as mail (POP and SMTP), telnet, ftp, Web (HTTP), news (NNTP), ping, and many more are supported.

The simplest form of IP masquerading firewall is two simple lines:

```
ipfwadm -F p deny
ipipfwadm -F a masquerade -S 192.168.1.0/24 -D 0.0.0/0
```

These are known as “F” order rules. The first line sets up a default policy (-p) to “deny” all connections unless specifically stated. You can also do a default policy of “accept,” but this would defeat the purpose of the firewall.
The second line appends (-a) a masquerade (m) policy from the source (-S) of 192.168.1.0/24. This is our local Ethernet network, with a mask of 255.255.255.0 The 24 means that the first 24 bits of a 32-bit IP are set, thus a netmask of 255.255.255.0. The destination of 0.0.0/0, pretty much represents everything else in the world.

If we wanted only a few machines on the local network to have access to the Internet via the Linux box, the second line could be replaced with

```
ipfwadm -F a m -S <local machine IP>/32 -D 0.0.0/0
```