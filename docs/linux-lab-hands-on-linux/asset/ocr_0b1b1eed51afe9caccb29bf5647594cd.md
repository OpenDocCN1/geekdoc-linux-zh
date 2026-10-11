![](bbox=[0.2, 0.14, 0.85, 0.155])

```
`/etc/protocols`
```

![](bbox=[0.2, 0.175, 0.85, 0.19])

It lists protocols available on your system.

![](bbox=[0.2, 0.205, 0.85, 0.22])

```
`/etc/mdprobe.conf`
```

![](bbox=[0.2, 0.235, 0.85, 0.25])

The above file is used for Ethernet module configuration.

# ## TCP/IP Configuration Addresses

The following are the different addresses used in TCP/IP configuration:

+   - **Host address**: Represents the IP address of your system; it has a network part to identify the network you are on and a host part to identify your own system.
+   - **Network address**: Represents the IP address of your network.
+   - **Broadcast address**: Represents the IP address for sending messages to all hosts on your network at once.
+   - **Gateway address**: Represents the IP address of your gateway system, if you have one (usually the network part of your host IP address with the host part set to 1).
+   - **Domain name server addresses**: Represents the IP addresses of domain name servers your network uses.
+   - **Netmask**: Determines the network and host parts of your IP address.

Interface Configuration

# ## Configuring NIC's IP Address

When we have many computers on a network, you need way to identify each one uniquely. In TCP/IP networking, the address assigned to each computer is known as IP address. IP address is the logical address used to communicate with people, computers, and devices and gather information. IP address is used to send and receive information from one host to another through a physical medium such as, cable on the network. An IP address is a unique 32 bit logically assigned binary number of four octets, which is represented in dotted decimal notation, designated to a particular device. Hosts and routers (a device used to determine the destination of a data packet) used in the TCP/IP protocol suite are identified by the IP address. The IP address is also divided into classes and each class has its specific range. The IP address consists of two parts, which are as follows:

+   - **Network ID**: Identifies the network to which the host is connected. Network ID is the same for all the hosts on a particular network.
+   - **Host ID**: Identifies the host on the network. Host ID is different for different hosts on the network.

**Table 1 : Division of IP Addresses**

| IP Address   | Network ID | Host ID |
|:-------------|:-----------|:--------|
| 193.168.75.38 | 193.168.75 | 38      |
| 130.11.45.90 | 130.11     | 45.90   |
| 125.25.210.12 | 125        | 25.21.12|