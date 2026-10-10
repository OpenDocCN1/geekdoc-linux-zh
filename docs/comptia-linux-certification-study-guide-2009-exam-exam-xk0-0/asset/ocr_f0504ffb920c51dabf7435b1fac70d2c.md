although there are many more, and the complete list can be found by typing `man dhcp-options`.

```
#
#sample configuration file for dhcpd
#
#option definitions common to all supported networks...
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

#set the time a client can keep the IP address
default-lease-time 600;
max-lease-time 7200;

#if this DHCP server is the official DHCP server for the local
# network, the authoritative directive should be uncommented.
#authoritative;

#set the default gateway to be used by clients
option routers 10.254.239.1;

#set up the NTP server
option ntp-server 10.254.239.6;

#set the nameserver to be used by the clients
option domain-name-servers 10.254.239.5

#set up a WINS client for Microsoft Windows clients
option netbios-name-servers 10.254.239.3;

#this is a very basic subnet declaration.

subnet 10.254.239.0 netmask 255.255.255.224 {
 range 10.254.239.10 10.254.239.20;
 option routers rtr-239-0-1.example.org, rtr-239-0-2.example.org;
}

#a network set-up for future use, but not currently used.
subnet 10.254.240 netmask 255.255.255.0 {
}

#Fixed IP addresses can also be specified for hosts.
#names or IP addresses can be used
```