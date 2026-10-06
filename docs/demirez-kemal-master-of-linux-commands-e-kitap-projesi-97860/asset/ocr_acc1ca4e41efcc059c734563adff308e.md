# Kemal Demirez | 241

```
root@kemal:~# ping -c 3 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=24 ms
bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=24.7 ms
bytes from 192.168.1.2: icmp_seq=3 ttl=64 time=99.4 ms
-
-
192.168.1.2 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 202ms
tr min/avg/max/mdev = 2.474/75.369/124.170/52.523 ms
```

# Traceroute

The traceroute command shows us all hosts/routers which the network packet goes through while reaching the destination. For example, let your traceroute google.com command.

```
root@kemal:~# traceroute google.com
tracoute to google.com (216.58.211.46), 30 hops max, 60 packet bytes
1 192.168.1.1 (192.168.1.1) 3.862 ms 5.689 ms 6.990 ms
2 ***
3 ***
4 ***
5 ***
6 ***
7 ***
8 72.141.214.246 (72.141.214.246) 87.869 ms 90.097 ms 90.206 ms
9 209.85.252.186 (209.85.252.186) 90.808 ms 96.036 ms 96.128 ms
10 ***
11 ***
12 ***
13 ***
14 ***
15 209.85.142.16 (209.85.142.16) 103.588 ms 106.944 ms
16 ***
17 muc03s14-in-f4.1le100.net (216.58.211.46) 123.965 ms 125.070 ms
s
```

# Netstat

To list the network connections, routing tables, etc. information we use netstat command. This command can be used with diffrent parameters, however the preferred usage to get the information about the links in the system is netstat - antp.