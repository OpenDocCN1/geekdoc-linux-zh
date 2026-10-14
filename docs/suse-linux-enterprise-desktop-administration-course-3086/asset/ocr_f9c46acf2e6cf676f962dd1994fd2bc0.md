Packets that cannot be sent according to previous entries in the routing table are sent through the gateway 10.0.0.254.

To delete an entry from the routing table, use a command similar to the following:

```
da2:~ # ip route delete 192.168.1.0/24 dev eth0
```

This command deletes the route to the network **192.168.1.0** assigned to the device **eth0**.

![](bbox=[0.104, 0.249, 0.294, 0.322])

The ip command allows you to abbreviate the options as long as they remain unambiguous. Usually one or two letters are enough. The above command can be abbreviated to `ip r s eth0 down`.

Changes made with the ip command are lost with the next reboot. To make permanent changes, use the YaST Network Card module. It writes the changes to files in the directory /etc/sysconfig/network/. It is possible to change these files with an editor, but this is beyond the scope of this course.

# Test Network Connections with ping

The tool ping lets you check network connections between two hosts in a simple way. If the ping command works, then both the physical and logical connections are correctly set up between the two hosts.

The ping command sends special network packets to the target system and waits for a reply. In the simplest scenario, you enter ping with an IP address:

```
ping 10.0.0.10
```

You can also use the hostname of the target system instead of an IP address. The output of ping looks similar to the following:

```
PING 10.0.0.10 (10.0.0.10) 56(84) bytes of data.
64 bytes from 10.0.0.10: icmp_seq=1 ttl=60 time=2.95 ms
64 bytes from 10.0.0.10: icmp_seq=2 ttl=60 time=2.16 ms
64 bytes from 10.0.0.10: icmp_seq=3 ttl=60 time=2.18 ms
64 bytes from 10.0.0.10: icmp_seq=4 ttl=60 time=2.08 ms
```

Each line of the output represents a packet sent by ping. ping keeps sending packets until it is terminated by pressing Ctrl+c.

The output displays the following information:

+   - The size of an ICMP datagram (64 bytes).
+   - The IP address of the target system (from 10.0.0.10).
+   - The sequence number of each datagram (seq=1).
+   - The TTL (Time To Live) of the datagram (ttl=60).