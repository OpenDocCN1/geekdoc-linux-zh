After the file is configured, the service to be started (or restarted) is **isc-dhcp-server** on Ubuntu/Debian-based systems and **dhcpd** on RHEL-based systems. Using the command `journaltl` to check the logs from the system, it will be possible to obtain information about the requests and the IP addresses assigned, as is shown in the following excerpt:

```
dhcpd[1151]: Server starting service.

dhcpd[1151]: DHCPDISCOVER from 52:54:00:57:d0:9f via enp8s0

dhcpd[1151]: DHCPOFFER on 192.168.100.222 to 52:54:00:57:d0:9f via enp8s0

dhcpd[1151]: DHCPREQUEST for 192.168.100.222 (192.168.100.1) from 52:54:00:57:d0:9f via enp8s0

dhcpd[1151]: DHCPACK on 192.168.100.222 to 52:54:00:57:d0:9f via enp8s0
```

As a client to test the **DHCP requests**, the utility `dhclient` offers the possibility to configure one interface with a dynamic IP instead, to use the system configuration (using files, **NetworkManager**, or `netplan`). This utility allows to specify the option `-v` to enable verbose logging. The option `-r` is used to release the current lease and stop the client running for the interface. *Figure 9.6* shows an example of the usage, and the output is shown:

```
[root@rhel ~]# dhclient -v enp7s0
Internet Systems Consortium DHCP Client 4.4.2bi
Copyright 2004-2019 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp7s0/52:54:00:57:d0:9f
Sending on LPF/enp7s0/52:54:00:57:d0:9f
Sending on Socket/fallback
DHCPDISCOVER on enp7s0 to 255.255.255.255 port 67 interval 5 (xid=0x464c887f)
DHCPOFFER of 192.168.100.222 from 192.168.100.1
DHCPREQUEST for 192.168.100.222 on enp7s0 to 255.255.255.255 port 67 (xid=0x464c887f)
DHCPACK of 192.168.100.222 from 192.168.100.1 (xid=0x464c887f)
bound to 192.168.100.222 -- renewal in 284 seconds.
```

# Figure 9.6: Output example for command dhclient

The files where the DHCP server keeps the leases in the files are `/var/dhcp/lib/dhcpd.leases` for IPv4 and `/var/lib/dhcp/dhcpd6.leases` for IPv6. For the software `dnsmasq`, it is required to install the package with the same name. The main configuration is `/etc/dnsmasq.conf`, which is used for configuration not only for DHCP but also for DNS and TFTP. This file can contain configuration for IPv6 too. An example of configuration to provide DHCP service is shown in the following excerpt:

```
listen-address=192.168.100.1
domain=mycompany.com
```