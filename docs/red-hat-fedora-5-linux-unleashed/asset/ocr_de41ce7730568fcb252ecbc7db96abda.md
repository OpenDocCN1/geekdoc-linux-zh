Using the -n option to the route command will give the same information substituting IP addresses for names and asterisks (*) and looks like this:

```
# /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref Use Iface
149.112.50.64   0.0.0.0         255.255.255.192 U     0     0     0  eth0
208.59.243.0    0.0.0.0         255.255.255.0 U     0     0     0  eth0
127.0.0.0       0.0.0.0         255.0.0.0         U     0     0     0  lo
0.0.0.0         149.112.50.65   0.0.0.0         UG    0     0     0  eth0
```

The route command can add to the table using the add option. With the add option, you can specify a host (-host) or a network (-net) as the destination. If no option is used, the route command assumes that you are configuring the host issuing the command. The most common uses for the route command are to add the default gateway for a host, for a host that has lost its routing table, or if the gateway address has changed. For example, to add a gateway with a specific IP address, you could use the following:

```
# /sbin/route add default gw 149.112.50.65
```

Note that you could use a hostname instead of an IP address if desired. Another common use is to add the network to the routing table right after using the ifconfig command to configure the interface. Assuming that the 208.59.243.0 entry from the previous example was missing, replace it using the following command:

```
# /sbin/route add -net 208.59.243.0 netmask 255.255.255.0 dev eth0
```

You also can use /sbin/route to configure a specific host for a direct (point-to-point) connection. For example, say that you have a home network of two computers. One of the computers has a modem through which it connects to your business network. You typically work at the other computer. You can use the route command to establish a connection through specific hosts using the following command:

```
# /sbin/route add -host 198.135.62.25 gw 149.112.50.65
```

The preceding example makes the computer with the modem the gateway for the computer you are using. This type of command line is useful if you have a gateway or firewall connected to the Internet. There are many additional uses for the route command, such as manipulating the default packet size. See the man page for those uses.

```
/bin/netstat
```

The netstat command is used to display the status of your network. It has several parameters that can display as much or as little information as you prefer. The services are listed by sockets (application-to-application connections between two computers). You can use netstat to display the information in Table 18.2.