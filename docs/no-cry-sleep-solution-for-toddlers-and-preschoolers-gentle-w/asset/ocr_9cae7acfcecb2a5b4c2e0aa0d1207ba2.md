```
host rabbit {
    option host-name "rabbit.mytrek.com"
    hardware ethernet 00:80:AD:30:17:2A;
    fixed-address rabbit.mytrek.com;
}
host lizard {
    option host-name "lizard.mytrek.com"
    hardware ethernet 00:70:2b:4b:29:14;
    fixed-address 192.168.0.3;
}
```

A host declaration can also be placed within the subnet declaration to provide information about particular hosts in that subnet.

A common candidate for a fixed address is the DNS server for a network. Usually, you would want the DNS server located at the same IP address, so that it can be directly accessed. The DHCP server can then provide this IP address to its clients.

| Entries | Description |
|---|---|
| Declarations | |
| shared-network name | Used to indicate if some subnets share the same physical network |
| subnet subnet-number netmask | References an entire subnet of addresses |
| range [ dynamic-bootp ] low-address [ high-address ]; | Provides the highest and lowest dynamically allocated IP addresses |
| host hostname | References a particular host |
| group | Lets you label a group of parameters and declarations and then use the label to apply them to subnets and hosts |
| allow unknown-clients; deny unknown-clients; | Does not dynamically assign addresses to unknown clients |
| allow bootp; deny bootp; | Determines whether to respond to bootp queries |
| allow booting; deny booting; | Determines whether to respond to client queries |
| Parameters | |
| default-lease-time time; | Length in seconds assigned to a lease |
| max-lease-time time; | Maximum length of lease |
| hardware hardware-type hardware-address; | Network hardware type (Ethernet or token ring) and address |
| filename "filename"; | Name of the initial boot file |
| server-name "name"; | Name of the server from which a client is booting |
| next-server server-name; | Server that loads the initial boot file specified in the filename |
| TABLE 35-1 DHCP Declarations, Parameters, and Options |