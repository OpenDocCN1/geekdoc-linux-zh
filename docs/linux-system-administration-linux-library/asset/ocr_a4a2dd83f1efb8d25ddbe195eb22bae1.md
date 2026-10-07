# Chapter 4 Tools of the Trade

The route command is used to display and manipulate the IP routing table. It is primarily used to set up static routes to hosts or networks already configured by the ifconfig command.

ftp

```
ftp [options] host
```

The ftp command starts the interface to the Internet's File Transfer Protocol, allowing users to transfer files to and from a remote site. It is typically run interactively, although this can be turned off with the -i option.

telnet

```
telnet [options] [host|port]
```

The telnet command uses the Telnet protocol to communicate with the specified host or in command mode if no host is given. In command mode, telnet takes commands like OPEN (to open a host site), CLOSE (to close a host site), QUIT (exits the telnet session completely), STATUS, and a few others.

traceroute

```
traceroute [options] destination_host
```

The traceroute command allows you to determine how long a packet takes to make each hop along the way to the destination host. This is very helpful information when a transmission to that host is significantly delayed or not received at all. Each intermediate host is listed with the time (in milliseconds) that the hop took. Listing 4.7 shows sample output.

**Listing 4.7** Sample Output from the traceroute command

```
traceroute 216.15.152.66 (216.15.152.66), 30 hops max, 38 bytes
  packets
1 lvhun1.popsite.net (216.126.175.4) 107.606 ms 98.544 ms
  99.231 ms
2 bhm1-core1.popsite.net (216.126.175.1) 106.141 ms
  109.084 ms 109.090 ms
3 atl-core1-s1-3.popsite.net (216.126.168.221) 116.211 ms
  108.875 ms 109.361 ms
```