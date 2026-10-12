A single server at address 10.0.0.1 is used as the router (or gateway) and DNS server for the LAN. To ensure that this server always gets the fixed address of 10.0.0.1, a host entry is set to the hardware address (00:D0:B3:79:B5:35) for the Ethernet card on the host named *ns*.

The pool of addresses handed out by this DHCP server is 10.0.0.150 to 10.0.0.225, as set by the *range dynamic-bootp* line. (Using *dynamic-bootp* allows bootp and dhcp clients to get addresses.) Along with the IP address that each client is assigned, the client is also given the associated subnet-mask and domain name.

The IP addresses that the DHCP server hands out are leased to each client for a particular time. The *default-lease-time* (set to 21,600 seconds here, or six hours) is the time assigned if the client doesn't request a particular lease period. The *max-lease-time* (43,200 seconds here, or 12 hours) is the highest amount of time the server will assign, if the client requests it. Clients can renew leases, so they don't have to lose the IP address while they are still using it.

# ## Expanding the *dhcpd.conf* file

As I noted earlier, this is a very simple example that works well for a single network of client computers. Below are some examples of ways that you can expand your *dhcpd.conf* file.

+   -   If you have multiple ranges of addresses on the same subnetwork, you can add multiple range options to a subnet declaration. Here is an example:

```
```
    subnet 10.0.0.0 netmask 255.0.0.0 {
        range 10.0.0.10 10.0.0.100;
        range 10.0.0.200 10.0.0.250;
    }
```
```

This example causes the DHCP server to assign IP addresses between the ranges of 0.0.10 and 0.0.100 and between 0.0.200 and 0.0.250 on network *number* 10.

+   -   You can set fixed addresses for particular host computers. In particular, you would want to do this for your server computers so that their addresses don't change. One way to do this is based on the Ethernet hardware address of the server's Ethernet card. All information for that computer can be contained in a host definition, such as the following:

```
```
host pine {
    hardware ethernet 00:04:5A:4F:8E:47;
    fixed-address 10.0.0.254;
}
```
```

Here, when the DHCP server encounters the Ethernet address, the *fixed-address* (10.0.0.254) is assigned to it. Type *ifconfig -a* on the server computer to see the address of its Ethernet hardware (while the interface is up). Within this host definition, you can add other options as well. For example, you could set the location of different routes (*routers* option).