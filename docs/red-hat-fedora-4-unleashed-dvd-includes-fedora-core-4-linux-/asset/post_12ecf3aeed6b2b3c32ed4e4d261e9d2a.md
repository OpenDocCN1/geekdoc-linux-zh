
## Figure 17.2
Highlight an existing entry, and then click the Edit button to change /etc/hosts entries in the Hosts tab of the Network Configuration screen.

![img/774d40fd20903495c5cd00e2efad3f33_509_0.png](img/774d40fd20903495c5cd00e2efad3f33_509_0.png)

## Figure 17.3
Configure an Ethernet device in the Configure Network Setting screen of the Add New Device Type dialog.

![img/774d40fd20903495c5cd00e2efad3f33_509_1.png](img/774d40fd20903495c5cd00e2efad3f33_509_1.png)

# Dynamic Host Configuration Protocol

As the name implies, Dynamic Host Configuration Protocol (DHCP) configures hosts for connection to your network. DHCP allows a network administrator to configure all TCP/IP parameters for each host as he connects to the network after activation of a NIC. These parameters include automatically assigning an IP address to a NIC, setting name server entries in /etc/resolv.conf, and configuring default routing and gateway information for a host. This section first describes how to use DHCP to obtain IP address assignment for your NIC, and then how to quickly set up and start a DHCP server using Fedora.

> You can learn more about DHCP by reading RFC2131 “Dynamic Host Configuration Protocol.” Browse to http://www.ietf.org/rfc/rfc2131.txt.

## How DHCP Works

DHCP provides persistent storage of network parameters by holding identifying information for each network client that might connect to the network. The three most common pairs of identifying information are:

- **Network subnet/host address**—Used by hosts to connect to the network at will
- **Subnet/hostname**—Enables the specified host to connect to the subnet
- **Subnet/hardware address**—Enables a specific client to connect to the network after getting the hostname from DHCP

DHCP also allocates to clients temporary or permanent network (IP) addresses. Once a temporary assignment, known as a *lease*, has elapsed, the client can request to have the lease extended, or, if the address is no longer needed, the client can relinquish the address. For hosts that will be permanently connected to a network with adequate addresses available, DHCP allocates infinite leases.

DHCP offers your network some advantages. First, it shifts responsibility for assigning IP addresses from the network administrator (who can accidentally assign duplicate IP addresses) to the DHCP server. Second, DHCP makes better use of limited IP addresses. If a user is away from the office for whatever reason, the user's host can release its IP address for use by other hosts.

Like most things in life, DHCP is not perfect. Servers cannot be configured through DHCP alone because DNS does not know what addresses that DHCP assigns to a host. This means that DNS lookups are not possible on machines configured through DHCP alone; therefore, services cannot be provided. However, DHCP can make assignments based on DNS entries when using subnet/hostname or subnet/hardware address identifiers.

> The problem of using DHCP to configure servers using registered hostnames is being addressed by Dynamic DNS which, when fully developed, will enable DHCP to register IP addresses with DNS. This will allow you, for example, to register a domain name (such as imalinuxuser.com) and be able to easily access that domain's web server without needing to use static IP addressing of a specific host. The largest hurdle to overcome is the security implication of enabling each host connecting to the system to update DNS. A few companies, such as http://www.dyndns.org, are already offering Dynamic DNS services and have clients for Linux.

# Activating DHCP at Installation and Boot Time

During installation, you can instruct the Fedora installer to save DHCP settings for your NIC. After installation, you can also use the system-config-network client to edit the TCP/IP configuration information required to properly initialize and configure your NIC to connect your system to the local network and Internet. When you select a dynamic, or DHCP-assigned IP addressing scheme for your NIC, the broadcast address is set at 255.255.255.255 because dhclient, the DHCP client used for IP configuration, is initially unaware of where the DHCP server is located, so the request must travel every network until a server replies.

DHCP-specific information is simply saved as a BOOTPROTO=dhcp entry for your NIC under the /etc/sysconfig/network directory (in settings and scripts for a specific device, such as eth0).

Other settings specific to obtaining DHCP settings are saved in the file named dhclient.conf under the /etc directory and are documented in the dhclient.conf man page. More than 100 options are also documented in the dhcp-options man page.

However, using DHCP is not that complicated. If you want to use DHCP and know that there is a server on your network, you can quickly configure your NIC by using the dhclient like so:

```bash
# dhclient
Internet Software Consortium DHCP Client V3.0pl2
Copyright 1995-2001 Internet Software Consortium.
All rights reserved.
For info, please visit http://www.isc.org/products/DHCP
Listening on LPF/lo/
Sending on LPF/lo/
Listening on LPF/eth0/00:a0:24:aa:f5:17
Sending on LPF/eth0/00:a0:24:aa:f5:17
Sending on Socket/fallback
DHCPOFFER on eth0 from 192.168.2.254
DHCPACK from 192.168.2.254
save_previous /etc/yp.conf
save_previous /etc/resolv.conf
bound to 192.168.2.253 -- renewal in 9906 seconds.
```

In this example, the first Ethernet device, eth0, has been assigned an IP address of 192.168.2.253 from a DHCP server at 192.168.2.254. The renewal will take place in about two hours and 45 minutes.

> **NOTE**
> The file named dhcpd under the /etc/sysconfig directory can contain any optional command-line arguments, such as NIC lease times (the amount of time an interface has an assigned address). See the dhcpd manual page for options.

# DHCP Software Installation and Configuration

Installation of the DHCP client and server might be easiest during the initial install of Fedora, but you can also use RPMs later on, or download and build the source code yourself. The RPMs are available on your Fedora CD-ROMs or from a mirror FTP site (refer to Chapter 7 for more information). This section describes configuring the `dhclient` and setting up and running the `dhcpd` daemon.

## DHCP `dhclient`

As previously mentioned, DHCP use for an installed NIC is easily accomplished when installing Fedora on your host (read more about installation in Chapter 3, “Installing Fedora”), and during the network step of installation, you can choose to have DHCP initiated at boot time. If you choose to do this (and choose to install the DHCP client package), the DHCP client, `dhclient`, will send a broadcast message that the DHCP server will reply to with networking information for your host. That is it; you’re done.

If you choose to install from source, you will have to (as `root`) download and install the server packages that include `dhclient`. Unpack the source file, run `./configure` from the root of the source directory, run `make`, and then run `make install`. This should put the DHCP client binaries where they will start at the correct time in the boot process.

You can, however, fine-tune how `dhclient` works, and where and how it obtains or looks for DHCP information. You probably will not need to take this additional effort; but if you do, you can create and edit a file named `dhclient.conf`, and save it in the `/etc` directory with your settings. A few of the `dhclient.conf` options include:

- `timeout time ;`—How long to wait before giving up trying (60 seconds is the default)
- `retry time ;`—How long to wait before retrying (5 minutes is the default)
- `select-timeout time ;`—How long to wait before selecting a DHCP offer (0 seconds is the default)
- `reboot time ;`—How long to wait before trying to get a previously set IP (10 seconds is the default)
- `renew date ;`—When to renew an IP lease, where `date` is in the form of `<weekday><year>/<month>/<day> <hour>:<minute>:<second>`, such as `4 2004/1/1 22:01:01` for Thursday, January 4, 2004 at 10:01 p.m.

See the `dhclient.conf` man page for more information on additional settings.

## DHCP Server

Again, the easiest way to install the DHCP server on your computer is to include the RPMs at install time or to use RPMs if you’ve installed your machine without installing the DHCP server RPMs. If you are so inclined, you can go to the Internet Software Consortium (ISC) website and download and build the source code yourself ([http://www.isc.org](http://www.isc.org)).
