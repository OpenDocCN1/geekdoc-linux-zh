Things get more complicated when you begin looking at tenant networking, which our deployments have. For the tenant network (our default is the 10.190.0.0/24 network), you will not see the IP addresses or devices by simply using the ip command on your controller node. Instead, these networks live in network name spaces that need to be accessed with the ip netns command. For example, in order to see the network where the DHCP server runs you’ll need to use:

```
$ sudo ip netns
grouter-1c1c7574-9116-438f-aa33-1eb9694f8f5a
gdhcp-961c7aa2-4c7b-452f-bc65-6b7cb2b9798a
```

The name space ID for the DHCP server begins with gdhcp-. In order to run commands in this name space to view details about and manipulate that network, you will use the exec command with the name space ID and the command you wish to run. The following runs ip addr on the qdhcp network name space:

```
$ sudo ip netns exec gdhcp-961c7aa2-4c7b-452f-bc65-6b7cb2b9798a ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
13: tap4c049b01-c0- <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1400 qdisc noqueue state UNKNOWN group default
link/ether f a:16:3e:83:01:c6 brd ff:ff:ff:ff:ff:ff
inet 10.190.0.5/24 brd 10.190.0.255 scope global tap4c049b01-c0
valid_lft forever preferred_lft forever
inet6 fe80::f816:3e83:ic6/64 scope link
valid_lft forever preferred_lft forever
```

As you learned in the networking chapter, the tap interface here is what has the address for your DHCP server. A test you can use to see if a new instance can effectively ping may be to ping this address from your instance, or to confirm you can ping the gateway for this network.

```
$ sudo ip netns exec gdhcp-961c7aa2-4c7b-452f-bc65-6b7cb2b9798a ping -c 2 10.190.0.1
PING 10.190.0.1 (10.190.0.1) 56(84) bytes of data.
64 bytes from 10.190.0.1: icmp_seq=1 ttl=64 time=0.322 ms
64 bytes from 10.190.0.1: icmp_seq=2 ttl=64 time=0.054 ms

--- 10.190.0.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 0.054/0.188/0.322/0.134 ms
```

As you can see, various commands can be run using this network, and so it’s very valuable for testing connectivity on these network name spaces that may seem invisible otherwise.

You may have noticed there is also a name space ID that begins with grouter-. This name space is used to provide routing at Network Address Translation (NAT) between the private instance tenant network and the external provider network. Go ahead and run similar exec commands on that interface and refer back to the networking chapter to learn more about what is happening.