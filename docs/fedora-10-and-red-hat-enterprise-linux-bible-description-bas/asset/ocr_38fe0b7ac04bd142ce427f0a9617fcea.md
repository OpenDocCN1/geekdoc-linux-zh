# Chapter 23: Setting Up a DHCP Boot Server 913

```
range 10.0.0.10 10.0.0.100;
range 10.0.0.200 10.0.0.250;
}
```

This example causes the DHCP server to assign IP addresses between the ranges of 10 and 100 between 200 and 250 on network 10.0.0.

+   You can set fixed addresses for particular host computers, also called reservations. In particular, you would want to do this for your server computers so that their addresses don't change. While you could simply omit the fixed IP addresses from your pool of DHCP assigned addresses, you would lose some centralized management of IP configurations. The DHCP reservations allow you to centrally configure all IP address information. One way to do this is on the Ethernet hardware address of your server's Ethernet card. All information for that computer can be contained in a host definition, as the following:

```
host pine {
  hardware ethernet 00:04:5A:4F:8E:47;
  fixed-address 10.0.0.254;
}
```

Here, where the DHCP server encounters the Ethernet address, the fixed-address 10.0.0.254 is assigned to it. It's a good idea to statically assign server IP addresses using ifconfig -a on the computer to see the address of its Ethernet hardware (while the interface is up). Within this host definition, you can add other options as well. For example, you could set the location of different routes (routers option).

+   Many of the options enable you to define the locations of various server types. These options can be set globally or within particular host or subnet definitions. For example:

```
option netbios-name-servers 10.0.0.252;
option time-servers 10.0.0.253;
```

In these examples, the netbios-name-servers option defines the location of the WINS server (if you are doing Windows file and print serving using Samba). The time-servers option sets the location of a time server on your network.

+   The DHCP server can be used to provide the information an X Terminal or diskless workstation could use to boot up on the network. Following is an example of a definition you could use to start a computer on your network:

```
host map {
  filename "dwboot/maple.nb";n  hardware ethernet 00:04:5A:4F:8E:47;
  fixed-address 10.0.0.150;
}
```