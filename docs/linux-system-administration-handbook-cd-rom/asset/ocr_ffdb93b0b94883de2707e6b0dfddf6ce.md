# 5.1 TCP/IP

lems with most other programs, including X. You can add the Ethernet interface and give the IP address and netmask. Don't turn on the “Configure Interface with BOOTP,” but you can turn on the “Activate Interface at boot time.” BOOTP is a protocol intended to dynamically assign IP addresses at boot time. The interface should be configured at boot time, so that once the machine starts, you can use the Ethernet.

# PPP

The Point-to-Point Protocol (PPP) is the way to connect to the Internet or a TCP/IP network via a dial-up line. PPP is designed to work between two machines and two machines only. This makes it ideal for dial-up applications, or even connecting remote locations via a leased line. Many 56-Kb links use PPP to carry IP traffic over the line.

PPP depends on one machine running pppd server on one end of the phone line, and a ppp client running on the modem dialing up (yours). Unlike Ethernet, you have to configure the software differently, depending on whether you are the client or the server.

PPP doesn't have the overhead of Ethernet, since no MAC addresses are used. Also, some compression is added to the IP frames to boost the amount of data that can be sent in a packet.

Like Ethernet, PPP can carry more than just IP traffic and can route IPX, Appletalk, and DECNET along with IP over a PPP link. Linux does not really take advantage of this functionality, but not many need it.

# PPP Client

Setting up a PPP client requires a modem, phone line, PPP server at some other phone number, and PPP support compiled into the kernel. Check the dmesg command to see if PPP support has been compiled in it. You can also check /lib/modules/ directory for ppp.o and see if it was compiled as a module. If support is not compiled in it, recompile the kernel and reboot using the new kernel.

The quick way of verifying that a PPP connection works is by doing something similar to the following:

```
pppd connect -v "*" ATDTPHONE CONNECT "*" login: login word: pass-word: '\'
/dev/cual 38400 debug crtscts modem defaultroute
```