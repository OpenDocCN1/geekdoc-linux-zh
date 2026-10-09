```
$ ssh linuxserver'
$ hostname
linuxserver
$
```

# Show Open Network Connections

```
$ sudo lsof -Pni
```

The lsof command can not only be used to display open files, but open network ports, and network connections. The -P option prevents the conversion of port numbers to port names. The -n option prevents the conversion of IP addresses to host names. The -i option tells lsof to display network connections.

```
$ sudo lsof -Pni
COMMAND          PID USER   FD TYPE DEVICE SIZE/OFF
NODE NAME
dhclient      989 root   6u  IPv4  11522
0t0 UDP *:68

sshd          1202 root   3u  IPv4  12418
0t0 TCP *:22 (LISTEN)

sshd          1202 root   4u  IPv6  12423
0t0 TCP *:22 (LISTEN)

ntpd          1210 ntp  16u  IPv4  12464
0t0 UDP *:123

ntpd          1210 ntp  17u  IPv6  12465
0t0 UDP *:123

ntpd          1210 ntp  18u  IPv4  12476
0t0 UDP 127.0.0.1:123

ntpd          1210 ntp  19u  IPv4  12477
0t0 UDP 192.168.122.60:123
```