# Network Information: ping, finger, traceroute, and host

You can use the ping, finger, traceroute, and host commands to find out status information about systems and users on your network. ping is used to check if a remote system is up and running. You use finger to find out information about other users on your network, seeing if they are logged in or if they have received mail. host displays address information about a system on your network, giving you a system's IP and domain name addresses. traceroute can be used to track the sequence of computer networks and systems your message passed through on its way to you. Table 15-1 lists various network information tools.

Though not included with Red Hat, for the GNOME desktop, the GNOME Workstation Command Center utility provides a GNOME interface for entering the ping, traceroute, and host commands, among other features. On the K Desktop, you can use the KDE network utilities (knu) to issue ping, finger, traceroute, and host commands.

# ping

The ping command detects whether a system is up and running. ping takes as its argument the name of the system you want to check. If the system you want to check is down, ping issues a timeout message indicating a connection could not be made. The next example checks to see if www.redhat.com is up and connected to the network:

```
$ ping www.redhat.com
PING www.portal.redhat.com (206.132.41.231): 56 data bytes
64 bytes from 206.132.41.231: icmp_seq=0 ttl=248 time=24.0 ms
64 bytes from 206.132.41.231: icmp_seq=1 ttl=248 time=124.5 ms
64 bytes from 206.132.41.231: icmp_seq=2 ttl=248 time=77.9 ms
64 bytes from 206.132.41.231: icmp_seq=3 ttl=248 time=220.1 ms
64 bytes from 206.132.41.231: icmp_seq=4 ttl=248 time=14.9 ms

--- www.portal.redhat.com ping statistics ---
6 packets transmitted, 5 packets received, 16% packet loss
round-trip min/avg/max = 14.9/92.2/220.1 ms
```

You can also use ping with an IP address instead of a domain name. With an IP address, ping can try to detect the remote system directly without having to go through a domain name server to translate the domain name to an IP address. This can be helpful for situations where your network's domain name server may be temporarily down and you want to check if a particular remote host on your network is connected. In the next example, the user checks the Red Hat site using its IP address:

```
$ ping 206.132.41.231
PING 206.132.41.231 (206.132.41.231): 56 data bytes
64 bytes from 206.132.41.231: icmp_seq=0 ttl=248 time=16.6 ms
64 bytes from 206.132.41.231: icmp_seq=1 ttl=248 time=65.1 ms
64 bytes from 206.132.41.231: icmp_seq=2 ttl=248 time=70.1 ms
64 bytes from 206.132.41.231: icmp_seq=3 ttl=248 time=336.6 ms
64 bytes from 206.132.41.231: icmp_seq=4 ttl=248 time=53.6 ms
64 bytes from 206.132.41.231: icmp_seq=5 ttl=248 time=42.1 ms

--- 206.132.41.231 ping statistics ---
6 packets transmitted, 6 packets received, 0% packet loss
```