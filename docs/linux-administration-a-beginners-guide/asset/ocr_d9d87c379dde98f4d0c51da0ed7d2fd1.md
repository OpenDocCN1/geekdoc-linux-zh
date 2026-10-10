# netstat

Normally, the netstat program is used to display the status of all of the network connections on a host. However, with the `-r` option, it can also display the kernel routing table. You should note that most other UNIX-based operating systems require that you use this method of viewing routes.

Here is an example invocation of `netstat -r` and its corresponding output:

```
[root@arilIan /root]# netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags  MSS  Window  irtt  Iface
192.168.1.0     0.0.0.0       255.255.255.0   U      0    0       0     eth0
127.0.0.0       0.0.0.0       255.0.0.0       U      0    0       0     lo
default         192.168.1.1   0.0.0.0         UG     0    0       0     eth0
```

In this example, we see a simple configuration. The host has a single network interface card, is connected to the 192.168.1.0 network, and has a default gateway set to 192.168.1.1.

Like the route command, netstat can also take the `-n` parameter so that it does not perform host name resolution.