Once installed, the ISC DHCP server uses configuration files in `/usr/local/etc` to control its operation. The most important of these files are

+   `/usr/local/etc/rc.d/isc-dhcpd.sh` This file controls the startup of the server, as described in Chapter 16. The FreeBSD package installs a script called `isc-dhcpd.sh.sample`, so you must rename this script to have the system start the server automatically. Aside from renaming the file, chances are you won't have to edit it.

+   `/usr/local/etc/dhcpd.conf` This file is the main DHCP configuration file. The operations described in the sections "Basic DHCP Configuration" and "Assigning Static IP Addresses" relate to this file. As with the startup script, the file that appears immediately after installation bears an extra `.sample` extension; you must copy or rename this file to use the DHCP server.

+   `/usr/local/etc/rc.d/dhcpd.conf` This file contains startup options you can pass to the server, listed on two lines—`dhcpd_options` and `dhcpd_ifaces`. Chances are you won't need to touch this file, but if you want the server to listen to some network interfaces but not others, you can list the interfaces (such as `fxp0`) on the `dhcpd_ifaces` line.

The `dhcpd.conf` file consists of comments, which are lines that begin with pound signs (`#`); global options, which consist of an option name followed by one or more values; and subnet definitions, which are groupings of options that apply to specific subnets for which the DHCP server is responsible. Most noncomment lines in `dhcpd.conf` end in semicolons (`;`). The start and end of option blocks, such as subnet definitions, are exceptions to this rule. These lines use curly braces (`{ }`) to delineate where a block begins and ends, thus:

```
subnet 10.254.239.0 netmask 255.255.255.224 {
    range 10.254.239.10 10.254.239.20;
    option routers rtr-239-0-1.example.org, xtr-239-0-2.example.org;
}
```

Before starting the DHCP server, you must create a file in which it stores information on the leases it delivers. You can do this by typing `touch /var/db/dhcpd.leases`, which creates an empty file of that name. If you don't create this file, the server won't operate correctly.

# Basic DHCP Configuration

The `dhcpd.conf.sample` file that ships with FreeBSD is functional, but it's virtually certain that you'll have to adjust it to suit your needs. Some of the global options are reasonable defaults, but some need to be changed for your network. The sample file also includes active definitions for several subnets, which you must replace with your