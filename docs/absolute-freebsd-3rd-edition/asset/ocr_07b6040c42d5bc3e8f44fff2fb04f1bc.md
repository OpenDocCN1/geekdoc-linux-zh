diskless configuration yet, any DHCP server logs the MAC address of clients. You can get the client information from the leases file, `/var/db/dhcpd.leases`.

```
---snip---
① lease 198.51.100.10 {
    starts 6 2017/09/16 06:57:23;
    ends 6 2017/09/16 07:07:23;
---snip---
② hardware ethernet 08:00:27:d8:c1:1c;
    uid "\001\010\000\330\301\034";
    set vendor-class-identifier = "PXEClient:Arch:00000:UNDI:002001";
}
---snip---
```

This client has a MAC address of 08:00:27:d8:c1:1c ② and has been offered IP address 198.51.100.10 ①. Given this information, we can create a DHCP configuration to assign this host a static IP address and provide its boot information.

# DHCP Configuration: Specific Diskless Hosts

We configured basic DHCP services in Chapter 20. Here’s a sample dhcpd(8) configuration for a diskless client. This doesn’t go inside a subnet statement but is a top-level statement on its own, even if it’s on a subnet shared with nondiskless DHCP clients.

```
① group diskless {
    ② next-server 198.51.100.1;
    ③ filename "pxeboot";
    ④ option root-path "198.51.100.1:/diskless/1/";
    ⑤ host compute1.mvl.io {
        ⑥ hardware ethernet 08:00:27:d8:c1:1c  ;
        ⑦ fixed-address 198.51.100.101 ;
    }
}
```

We define a group called diskless ①. This definition will allow us to assign certain parameters to the group and then just add hosts to the group. Every host in the group gets those same parameters.