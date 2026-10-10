
# Configuring the /etc/dhcpd.conf File

Suppose you have a single pool of IP addresses that you want to distribute to a set of computers that are all on the same subnetwork. In other words, all the computers are connected to one switch or cluster of switches with no routing between the devices. Here is an example of a simple dhcpd.conf file:

```text
ddns-update-style interim;
ignore client-updates;

subnet 10.0.0.0 netmask 255.255.255.0 {

option routers					10.0.0.1;
option domain-name-servers	10.0.0.1;
option subnet-mask				255.255.255.0;
option domain-name				"example.com";

range 10.0.0.150 10.0.0.225;
default-lease-time 21600;
max-lease-time 43200;

# Set name server to appear at a fixed address
host ns {
next-server ns1.example.com;
hardware ethernet 00:00:B3:79:B5:35;
fixed-address 10.0.0.1;
}
}
```

In this example, this DHCP server provides IP addresses for client computers on a small LAN. The first two lines tell the DHCP server to update DNS records for the local domain if the server also gives out hostnames to the clients.

The DHCP server is serving a single LAN, represented by a 10.0.0.0 network address with a 255.255.255.0 netmask. Other data in this file defines what information the DHCP server will hand out to clients on this LAN.

A single server at address 10.0.0.1 is used as the router (or gateway) and DNS server for the LAN. To ensure that this server always gets the fixed address of 10.0.0.1, a host entry is set to the hardware address (00:00:B3:79:B5:35) for the Ethernet card on the host named ns. Using the MAC address as shown above along with the option deny unknown-clients, you can allow only specified MAC addresses to obtain DHCP leases.

The pool of addresses handed out by this DHCP server is 10.0.0.150 to 10.0.0.225, as set by the range line. Along with the IP address that each client is assigned, the client is also given the associated subnetmask and domain name.

The IP addresses that the DHCP server hands out are leased to each client for a particular time. The default-lease-time (set to 21,600 seconds here, or 6 hours) is the time assigned if the client doesn't request a particular lease period. The `max-lease-time` (43,200 seconds here, or 12 hours) is the highest amount of time the server will assign, if the client requests it. Clients can renew leases, so they don't have to lose the IP address while they are still using it.

# Expanding the dhcpd.conf File

As I noted earlier, this is a very simple example that works well for a single network of client computers. The following are some examples of ways that you can expand your dhcpd.conf file:

- If you have multiple ranges of addresses on the same subnetwork, you can add multiple range options to a subnet declaration. Here is an example:

```text
subnet 10.0.0.0 netmask 255.255.255.0 {
    range 10.0.0.10 10.0.0.100;
    range 10.0.0.200 10.0.0.250;
}
```

This example causes the DHCP server to assign IP addresses between the ranges of 10 and 100 and between 200 and 250 on network 10.0.0.

- You can set fixed addresses for particular host computers, also called address reservations. In particular, you would want to do this for your server computers so that their addresses don't change. While you could simply omit the fixed IP addresses from your pool of DHCP assigned addresses, you would lose centralized management of IP configurations. The DHCP reservations allow you to centrally configure all IP address information. One way to do this is based on the Ethernet hardware address of the server's Ethernet card. All information for that computer can be contained in a host definition, such as the following:

```text
host zarkov {
    hardware ethernet 00:04:5A:4F:8E:47;
    fixed-address 10.0.0.254;
}
```

- Here, when the DHCP server encounters the Ethernet address, the `fixed-address` 10.0.0.254 is assigned to it. It's a good idea to statically assign server IP addresses. Type `ifconfig -a` on the server computer to see the address of its Ethernet hardware (while the interface is up). Within this host definition, you can add other options as well. For example, you could set the location of different routers (`routers` option).

- Many of the options enable you to define the locations of various server types. These options can be set globally or within particular host or subnet definitions. For example:

```text
option netbios-name-servers 10.0.0.252;
option time-servers 10.0.0.253;
```

- In these examples, the `netbios-name-servers` option defines the location of the WINS server (if you are doing Windows file and print option sharing using Samba). The `time-servers` option sets the location of a time server on your network.

The DHCP server can be used to provide the information an X Terminal or diskless workstation could use to boot up on the network. The following is an example of a definition you could use to start such a computer on your network:

```text
host flashg {
    filename "/dwsboot/flashg.nb";
    hardware ethernet 00:04:5A:4F:BE:47;
    fixed-address 10.0.0.150;
}
```

In the previous example, the boot file used by the diskless workstation from the DHCP server is located at /dwsboot/flashg.nb. The hardware ethernet value identifies the address of the Ethernet card on the client. The client's IP address is set to 10.0.0.150. All of these lines are contained within a host definition, where the hostname is defined as flashg. (See Table 22-1 for descriptions of data types and the "Thin Clients" heading in Table 22-2 for other options that may be useful for configuring thin clients.)

# Adding Options

There are dozens of options you can use in the /etc/dhcpd.conf file to pass information from the DHCP server to DHCP clients. Table 22-1 describes data types you can use for different options. Table 22-2 describes options that are available.

**TABLE 22-1**

**Data Types**

| **Data Types** | **Description** |
|---|---|
| IP address | Enter IP addresses as either an IP address number (11.111.111.11) or a fully qualified domain name (compl.example.com). To use a domain name, the name must be resolvable to an IP address number. |
| int32, int16, int8, uint32, uint16, uint8 | Used to represent signed and unsigned 32-, 16-, and 8-bit integers |
| string | Enter a string of characters, surrounded by double quotes (" "). |
| Boolean | Enter true or false when a Boolean value is required. |
| data-string | Enter a string of characters in quotes ("client" ) or a hexadecimal series of octets (00:04:5A:4F:BE:47). |

Options contain values that are passed from the DHCP server to clients. Although Table 22-2 lists valid options, the client computer will not be able to use every value you could potentially pass to it. In other words, not all options are appropriate in all cases.

# Setting Up a DHCP Boot Server

**TABLE 22-2**

# DHCP Options

| Options | Descriptions |
| :--- | :--- |
| **Names, Addresses, and Time** | |
| `option host-name string;` | Indicates the name that the client computer can use to identify itself. It can either be a simple hostname (e.g., `zarkov`) or a fully qualified domain name (e.g., `zarkov.example.com`). You may use this in a host declaration, where a host computer is identified by an Ethernet address. |
| `option domain-name string;` | Identifies the default domain name the client should use to resolve DNS hostnames. |
| `option subnet-mask ip-address;` | Associates a subnetwork mask with an IP address, for example: `option 255.255.255.0 10.0.0.1;` |
| `option time-offset int32;` | Indicates the offset (in seconds) from Coordinated Universal Time (UTC). For example, a UTC offset for U.S. Eastern Standard Time is set as follows: `option time-offset -18000;` |
| **Servers and Routers** | |
| `option routers ip-address [ , ip-address... ];` | Lists, in order of preference, one or more routers connected to the local subnetwork. The client may refer to this value as the gateway. |
| `option domain-name-servers ip-address [ , ip-address... ];` | Lists one or more Domain Name System (DNS) servers that the client can use to resolve names into IP addresses. Lists servers in the order in which they should be tried. |
| `option time-servers ip-address [ , ip-address... ];` | Lists, in order of preference, one or more time servers that can be used by the DHCP client. |
| `option ien116-name-servers ip-address [ , ip-address... ];` | Lists, in order of preference, one or more IEN 116 name servers that can be used by the client. (IEN 116 name servers predate modern DNS servers and are considered obsolete.) |
| `option log-servers ip-address [ , ip-address... ];` | Lists one or more MIT-LCS UDP log servers. Lists servers in the order in which they should be tried. |
| | continued |
