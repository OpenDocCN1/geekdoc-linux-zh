Options contain values that are passed from the DHCP server to clients. Although Table 22-2 lists valid options, the client computer will not be able to use every value you could potentially pass to it. In other words, not all options are appropriate in all cases.

Table 22-2 is divided into the following categories:

+   Names, Addresses, and Time — These options set values that are used by clients to have their hostnames, domain names, network numbers, and time zones (offset from GMT) defined.
+   *   Servers and Routers — These options are used to tell DHCP clients where on the network to find routers and servers. Although more than a dozen server types are listed, most often you will just indicate the address of the router and the DNS servers the client will use.
+   *   Routing — These options indicate whether or not the client routes packets.
+   *   Thin Clients — These options are useful if DHCP is being used as a boot server for thin clients. A thin client may be an X Terminal or diskless workstation that has processing power, but no disk (or a very small disk) so it can’t store a boot image and a file system itself.

> **NOTE:** The Linux Terminal Server Project (LTSP) contains all the software you need to set up a server and thin clients. You can find a description of LTSP in *Linux Toys II* (Wiley Publishing, 2005). The Fedora K12Linux project (<https://fedorahosted.org/k12linux>) is an example of an LTSP-based project that provides educational tools to thousands of students in schools.

**Table 22-2: DHCP Options**

| Options | Descriptions |
| :--- | :--- |
| | Names, Addresses, and Time |
| option host-name string; | Indicates the name that the client computer can use to identify itself. It can either be a simple hostname (for example, `pine`) or a fully qualified domain name (for example, `pine.handleishistory.com`). You may use this in a host declaration, where a host computer is identified by an Ethernet address. |
| option domain-name string; | Identifies the default domain name the client should use to resolve DNS hostnames. |
| option subnet-mask ip-address; | Associates a subnetwork mask with an IP address. For example, `option 255.255.255.0 10.0.0.1;` |
| option time-offset int32; | Indicates the offset (in seconds) from Coordinated Universal Time (UTC). For example, a UTC offset for U.S. Eastern Standard Time is set as follows: `option time-offset -18000;` |