```
root@ubuntu:~# tcpdump --list-interfaces
1.enplso [Up, Running, Connected]
2.enp7s0 [Up, Running, Connected]
3.bridge0 [Up, Running, Connected]
4.any (Pseudo-device that captures on all interfaces) [Up, Running
5.10 [Up, Running, Loopback]
6.bluetooth-monitor (Bluetooth Linux Monitor) [Wireless]
7.nflog (Linux netfilter log (NFLOG) interface) [none]
8.nfqueue (Linux netfilter queue (NFQUEUE) interface) [none]
9.dbus-system (D-Bus system bus) [none]
10.dbus-session (D-Bus session bus) [none]
11.0vs-system [none, Disconnected]
```

Figure 8.29: Output example for the command tcpdump

+   Capture the traffic for the interface bridge0 not resolving IPs and ports and showing extra information (option -e) for each packet, exiting after receiving one packet. Refer to figure 8.30:

```
root@ubuntu:~# tcpdump -i bridge0 -n -e -c 1
tcpdump: verbose output suppressed, use -v(v)... for full protocol decode
listening on bridge0, link-type EN10MB (Ethernet), snapshot length 262144 byte:
20:00:01.759016 52:54:00:c8:55:25 > ff:ff:ff:ff:ff:ff, ethertype ARP (0x0806),
length 42: Request who-has 10.0.0.220 tell 10.0.0.218, length 28
1 packet captured
4 packets received by filter
0 packets dropped by kernel
```

Figure 8.30: Output example for the command tcpdump

+   Capture traffic and save it in a file using the option -w and read using the option -r, as shown in figure 8.31:

```
root@ubuntu:~# tcpdump -i bridge0 -n -e -c 1 -w example.cap
tcpdump: listening on bridge0, link-type EN10MB (Ethernet), snapshot length 26214:
bytes
1 packet captured
2 packets received by filter
0 packets dropped by kernel
root@ubuntu:~# tcpdump -r example.cap
reading from file example.cap, link-type EN10MB (Ethernet), snapshot length 26214:
20:04:08.503198 IP 10.0.0.218 > ubuntu.network-1: ICMP echo request, id 2, seq 1,
length 64
```

Figure 8.31: Output example for the command tcpdump

The arguments for the command tcpdump are expressions to define filters. Some of the popular ones are defined in table 8.5:

| Filter | Description |
| :---------------- | :------------------------------------ |
| [src / dst ] host | Filter the host, optionally indicating if it is an src or a dst. |