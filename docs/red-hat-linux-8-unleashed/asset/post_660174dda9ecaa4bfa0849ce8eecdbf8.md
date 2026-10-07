
# Dynamic Host Configuration Protocol

The RPMs are available on your Red Hat Linux CD-ROMs or from a Red Hat mirror FTP site (see Chapter 8 for more information). This section describes using the dhclient and dhcpd daemon.

## DHCP dhclient

DHCP use for an installed NIC is easily accomplished when installing Red Hat on your host (read more about installation in Chapter 3, “Installing Red Hat Linux”). During the network setup of installation, you can choose to have DHCP initiated at boot time. If you choose to do this (and choose to install the DHCP client package), the DHCP client, dhclient, will send a broadcast message that the DHCP server will reply to with network information for your host. That’s it; you’re done.

> Previous versions of Red Hat used the pump client dhclient to configure NICs using DHCP.

If you choose to install from source, you will have to (as root) download and install the server packages that include dhclient. Unpack the source file, run ./configure for the root of the source directory, run make, and then run make install. This should put the DHCP client binaries wherever they will start at the correct time in the boot process.

## DHCP Server

Again, the easiest way to install the DHCP server on your computer is to include the RPMs at install time or to use RPMs if you've installed your machine without installing the DHCP server RPMs. If you are inclined, you can go to the Internet Software Consortium (ISC) Web site and build the source code yourself.

If you decide to install from source downloaded from the ISC Web site, the installation is very straightforward. Just unpack your tar file, run ./configure from the root of the source directory, run make, and finally, if there are no errors, run make install. This will put all the files used by the DHCP daemon in the correct places. If you have the disk space, it’s best to leave the source files in place until you are sure that DHCP is running correctly; otherwise, you can delete the source tree.

> For whichever installation method you choose, ensure that a file called /etc/dhcpd.leases is created. The file may be empty, but it does not need to exist for dhcpd to start properly.

## Using DHCP to Configure Network Hosts

Configuring your network with DHCP offers some difficulty. Configuring the client is easy, but the server configuration takes a bit of work, depending on how complex your network is and how much you want DHCP to do.

# CHAPTER 13 Network Connectivity

## Using the dhclient Client

If you DHCP client software from RPM, no configuration used; DHCP will be ready to run. After configuration of the NIC use Red Hat's configuration tools or upon rebooting your system, run the command ifconfig -a, and you will see a new IP address assigned to your system's Ethernet device. Of course, a DHCP server must be running or accessing on your network, and this is discussed in the next section.

## DHCP Server Configuration

Configuring the server takes some thought and a little bit of work. Lucknow, the work only involves editing a single configuration file, /etc/dhcp.conf. To set up Red Hat and start the server at boot time, use the service, ntysv, or redhat-config-services commands.

The /etc/dhcp.conf file contains all the information needed to run dhcp. Red Hat includes a sample dhcp.conf in /usr/share/doc/dhcp-3.0pl1/dhcp.conf.sample. The DHCP server source files also contain a sample dhcp.conf file.

The /etc/dhcp.conf file can be looked at as a three-part file. The first part contains configurations for dhcp. The configurations include

- Setting the domain name-option domain-name "example.org"
- Setting DNS servers-option domain-name-servers ns1.example.org, ns2.example.org (IP addresses can be substituted).
- Setting the default and maximum lease times-default-lease-time 3600 and max-lease-time 14400.

Other settings in the first part include whether the server is the primary (authoritative) server and what type of logging DHCP should use. These settings are considered default and can be overridden by the subnet and which portion of the configuration in more complex situations.

> NOTE The dhcp.conf file requires semicolons (;) after each command statement. If your configuration file has errors or runs improperly, check for this.

The next part of dhcp.conf deals with the different subnets that your DHCP server serves; this section is quite straightforward. Each subnet is defined separately and can look like this:

```
subnet 10.5.5.0 netmask 255.255.255.224 {
option domain-name-servers ns1.internal.example.org;
option domain-name "internal.example.org";
option routers 10.5.5.1;
```

# Dynamic Host Configuration Protocol

```
option broadcast-address 10.5.5.31;
default-lease-time 600;
max-lease-time 7200;
```

This defines the IP addressing for the 10.5.5.0 subnet. It defines the IP address ranging from 10.5.5.26 through to be dynamically assigned to hosts that reside on that subnet. This example shows that any TCP/IP option can be set from the subnet portion of the configuration file. It shows which DNS server the subnet will connect to, which can be good for DNS server load balancing, or which can be used to limit the hosts that can be reached through DNS. It defines the domain name.

> For whichever installation method you choose, ensure that a file called /etc/dhcpd.leases is created. The file may be empty, but it does not need to exist for dhcpd to start properly.
