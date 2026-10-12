| Data Types | Description |
| --- | --- |
| data-string | Enter a string of characters in quotes ("client1") or a hexadecimal series of octets (00:04:5A:4F:8E:47). |

Options contain values that are passed from the DHCP server to clients. Although Table 23-2 lists valid options, the client computer will not be able to use every value you could potentially pass to it. In other words, not all options are appropriate in all cases.

Table 23-2 is divided into the following categories:

+   * **Names, Addresses, and Time** — These options set values that are used by clients to have their host name, domain name, network numbers, and time (offset from GMT) defined.
+   * **Servers and Routers** — These options are used to tell DHCP clients where on the network to find routers and servers. Though more than a dozen server types are listed, most often you will just indicate the address of the router and the DNS servers the client will use.
+   * **Routing** — These options indicate whether or not the client routes packets.
+   * **Thin Clients** — These options are useful if DHCP is being used as a boot server for thin clients. A thin client may be an X Terminal or diskless workstation that has processing power, but no disk (or a very small disk) so it can't store a boot image and a file system itself.

# Table 23-2: DHCP Options

| Options | Descriptions |
| --- | --- |
| **Names, Addresses, and Time** |  |  |
| option host-name *string*; | Indicates the name that the client computer can use to identify itself. It can either be a simple host name (for example, *pine*) or a fully-qualified domain name (for example, *pine.handsonhistory.com*). You may use this in a *host* declaration, where a host computer is identified by an Ethernet address. |  |
| option domain-name *string*; | Identifies the default domain name the client should use to resolve DNS host names. |  |
| option subnet-mask *ip-address*; | Associates a subnetwork mask with an IP address. For example, option `255.0.0.0 10.0.0.1;`. |  |