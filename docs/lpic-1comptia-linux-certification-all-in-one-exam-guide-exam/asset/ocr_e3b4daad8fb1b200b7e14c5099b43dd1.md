At this point, your network interface is loaded and active. However, before you can use it, you have to configure it with the IP protocol. Let’s discuss how this is done next.

# # Configuring IP Parameters

Remember that you need to configure your network interface with four parameters in order for the system to participate on an IP-based computer network. These include the following:

+   - IP address
+   - Subnet mask
+   - Default gateway router address
+   - DNS server address

There are two different ways to do this. These are discussed in Table 15-1.
If you want to statically assign IP address parameters to a Linux system, you can use the ifconfig command. If ifconfig is entered without any options, it displays the current status of all network interfaces in the system, as shown in Figure 15-10.

| Option | Description | Advantages | Disadvantages |
| :--- | :--- | :--- | :--- |
| **Static address assignment** | In this configuration, you manually configure a network host with IP address parameters. | The address used by a particular host never changes. This option is usually used by servers in the network. | The host consumes the address regardless of whether the system is powered on or off. This strategy also requires a lot of legwork on the part of the system administrator. He or she has to visit each computer in the network and manually specify IP parameters. |
| **Dynamic address assignment** | In this configuration, a network host contacts a Dynamic Host Configuration Protocol (DHCP) server when it boots. The DHCP server dynamically assigns an IP address to the host for a specified period of time called a lease. | This option makes configuring IP parameters for a large number of network hosts very easy. Just power the system on and it gets its IP address information. It also conserves IP address usage. Addresses used by systems that are powered off can be reassigned to other network hosts. | You must have a DHCP server installed and configured before you can use this option. In addition, the address assigned to a particular host can change frequently, making it an unsuitable option for network infrastructure systems such as servers. Because of this, this option is usually used for workstations. |

Table 15-1 IP Address Assignment Options