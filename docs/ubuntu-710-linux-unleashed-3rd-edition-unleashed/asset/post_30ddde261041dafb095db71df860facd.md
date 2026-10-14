
Save your changes, and then restart the sshd server. (Refer to Chapter 11, "Automating Tasks," to see how to restart a service.) Remote users must now access the host through port 2224, which can be done using ssh's -p (port) option like so:

```
$ ssh -p 2224 remote_host_name_or_IP
```

## Network Organization

Properly organizing your network addressing process grows more difficult as the size of your network grows. Setting up network addressing for a Class C network with fewer than 254 devices is simple. Setting up addressing for a large, worldwide company with a Class A network and many different users can be extremely complex. If your company has fewer than 254 hosts (meaning any device that requires an IP address, including computers, printers, routers, switches, and other devices) and all your workgroups can share information, a single Class C network will be sufficient.

## Subnetting

Within Class A and B networks, there can be separate networks called subnets. Subnets are considered part of the host portion of an address for network class definitions. For example, in the 128. Class B network, you can have one computer with an address of 128.10.10.10 and another with an address of 128.10.200.20; these computers are on the same network (128.10.), but they have different subnets (128.10.10. and 128.10.200.). Because of this, communication between the two computers requires either a router or a switch. Subnets can be helpful for separating workgroups within your company.

Often subnets can be used to separate workgroups that have no real need to interact with or to shield from other groups' information passing among members of a specific workgroup. For example, if your company is large enough to have its own HR department and payroll section, you could put those departments' hosts on their own subnet and use your router configuration to limit the hosts that can connect to this subnet. This configuration prevents networked workers who are not members of the designated departments from being able to view some of the confidential information the HR and payroll personnel work with.

Subnet use also enables your network to grow beyond 254 hosts and share IP addresses. With proper routing configuration, users might not even know they are on a different subnet from their co-workers. Another common use for subnetting is with networks that cover a wide geographic area. It is not practical for a company with offices in Chicago and London to have both offices on the same subnet, so using a separate subnet for each office is the best solution.

## Subnet Masks

Subnet masks are used by TCP/IP to show which part of an IP address is the network portion and which part is the host. Subnet masks are usually referred to as netmasks. For a pure Class A network, the netmask would be 255.0.0.0; for a Class B network, the

## Network Interface Cards

A computer must have a network interface card (NIC) to connect to a network. Currently, there are several topologies (ways of connecting computers) for network connections. These topologies range from the old and mostly outdated 10BASE-2 to the much newer and popular wireless Wi-Fi or 802.11 networking.

## A Dual-Host No-NIC Network

The truly frugal can also “network” two Linux workstations using a null-modem or LPT cable and PPP as shown in the PPP HOWTO at http://tldp.org/HOWTO/PPP-HOWTO/direct.html. Just connect two PCs running Linux together with a null-modem cable, and use the pppd daemon on each end. If one Linux host is connected to a network or has a dial-up connection, that PC becomes a gateway for the other host. You have to use pppd’s defaultroute option on the serial-only host when connecting.

Each NIC has a unique address (the hardware address, known as media access control, or MAC), which identifies that NIC. This address is six pairs of hexadecimal bits separated by colons (:). A MAC address looks similar to this: 00:60:08:8F:5A:D9. The hardware address is used by DHCP (see “Dynamic Host Configuration Protocol” later in this chapter) to identify a specific host. It is also used by the Address Resolution Protocol (ARP) and Reverse Address Resolution Protocol (RARP) to map hosts to IP addresses.

This section covers some of the different types of NIC used to connect to your network.

## Token Ring

Token ring networking was developed by IBM. As the name implies, the network is set up in a ring. A single “token” is passed from host to host, indicating the receiving host’s permission to transmit data.

Token ring has a maximum transfer rate of 16Mbps (16 million bits per second). Unlike 10BASE-2 and 10BASE-5, token ring uses what is called unshielded twisted pair (UTP) cable. This cable looks a lot like the cable that connects your phone to the wall. Almost all token ring NICs are recognized by Linux.

## 10BASE-T

10BASE-T was the standard for a long time. A large number of networks still use it. 10BASE-T also uses UTP cable. Instead of being configured in a ring, 10BASE-T mostly uses a star architecture. In this architecture, the hosts all connect to a central location (usually a hub, which you learn about later in the section titled “Hubs and Switches”). All the data is sent to all hosts, but only the destination host takes action on individual packets. 10BASE-T has a transfer rate of 10Mbps.

10BASE-T has a maximum segment length of 100 meters. There are many manufacturers of 10BASE-T NICs, and most are recognized by Ubuntu.
