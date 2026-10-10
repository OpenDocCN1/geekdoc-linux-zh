
when the systems boot up. If your ISP or support staff has configured a DHCP server, you can be on the Internet faster than you can open your Web browser.

Setting up a DHCP server enables you to centrally manage the addresses and other network information for client computers on your private network. With DHCP configured on your network, a client computer can simply indicate that it wants to use DHCP and the DHCP server can provide its IP address, network mask, DNS server, NetBIOS server, router (gateway), and other information needed to get up and running on the network.

With DHCP, you can greatly simplify the initial network configuration that each client computer on your network needs to do. Later, as your network evolves, you can easily update that information, having changes automatically picked up by clients when they restart their network interfaces.

> NOTE: Although this chapter focuses on the configuration of DHCP client and server services on your Fedora systems, your Fedora DHCP client can use the services of other network devices. For example, you might have a Cisco router, a DSL/Cable device with DHCP services, or even a Windows-based DHCP server. DHCP clients for Fedora will not have trouble working with any standards-compliant DHCP server.

To configure the DHCP server described in this chapter, you need to have the `dhcp` package installed (`yum install dhcp`).

## Setting Up a DHCP Server

To configure a DHCP server you need to install the `dhcp` package. Assuming you have already set up the physical connections between your DHCP server and the client computers on your network (presumably an Ethernet LAN), the minimum tools you need to get the DHCP server working are:

- A firewall and SELinux settings that allow requests for DHCP service
- A configured `/etc/dhcp/dhcpd.conf` file
- A running `dhcpd` server daemon (which can be started at boot time)

After the DHCP server is running, it listens on UDP port 67 for requests from DHCP clients on the LAN. A client simply boots up (with an Ethernet network interface turned on and DHCP identified as its method of getting network addresses). This causes the client to send out a DHCP discovery request to `255.255.255.255` (the global broadcast address). The DHCP server picks up that request and feeds the client the information it needs to get up and running on the network.

> NOTE: The `dhcpd.conf` file can serve a wide range of configuration information to DHCP clients. To see the full set of options and parameters you can set in that file, refer to the `dhcp-options` and `dhcpd.conf` man pages (type `man dhcp-options`).

## Opening your firewall and SELinux for DHCP

The firewall on your DHCP server must be configured to allow access to UDP ports 67 and 68. The easiest way to do this is to select System → Administration → Firewall from the GNOME desktop. From the Firewall Configuration window that appears, enable the firewall, and then select Other Ports and add UDP ports 67 and 68.

If you prefer to use `iptables` directly to change your firewall, you can add a new rule to `iptables` and then save the changes permanently. Type the following as root user:

```bash
# iptables -I INPUT -i eth0 -p udp --sport 67:68 --dport 67:68 -j ACCEPT
```

In this example, requests are allowed to and from source and destination ports 67 and 68 (`--sport 67:68` and `--dport 67:68`) on the `eth0` interface (which is your first Ethernet card). DHCP uses the User Datagram Protocol (UDP) protocol (`-p udp`). If your DHCP server is also a routing firewall for your network, you want to make sure that you are only offering DHCP services to your LAN and not to the Internet. (You need to figure out if `eth0`, `eth1`, or some other card is connected to your LAN.)

If the rule was accepted (type `iptables -L -n` to make sure), you can save your entire firewall configuration so that the new rule is included permanently. To change your firewall, type the following (as root user):

```bash
# service iptables save
```

This updates your `/etc/sysconfig/iptables` file so that all the current rules (including the one you just added) are included the next time `iptables` is restarted. To restore those firewall settings without rebooting, use the `iptables-restore` command:

```bash
# iptables-restore < /etc/sysconfig/iptables
```

SELinux should not block normal operations of the `dhcpd` daemon. SELinux does, however, enforce that particular file contexts be set on dhcp configuration files. For example, type:

```bash
# ls -lZ /etc/dhcp/dhcpd.conf
-rw-r-----. root root system_u:object_r:dhcp_etc_t:s0 /etc/dhcp/dhcpd.conf
```

If you copied or moved your `dhcpd.conf` file from another location and it shows a context other than `dhcp_etc_t` or `dhcpd_etc_t`, you need to restore the proper context before the `dhcpd` service can start. You can do that by typing:

```bash
# restorecon -R /etc/dhcp
```

If you believe SELinux is still causing problems with your `dhcpd` service, and your environment does not require SELinux, consider setting SELinux to permissive. Open the SELinux Administration window (System → Administration → SELinux Management) and set enforcing mode to Permissive (both system default and current).

## Configuring the /etc/dhcp/dhcpd.conf file

Suppose you have a single pool of IP addresses that you want to distribute to a set of computers that are all on the same subnetwork. In other words, all the computers are connected to one switch or cluster of switches with no routing between the devices. Here is an example of a simple `dhcpd.conf` file:

```conf
ddns-update-style none;

option domain-name                "hands-onhistory.com";
option domain-name-servers        10.0.0.1, 10.0.0.2;
default-lease-time 21600;

subnet 10.0.0.0 netmask 255.255.255.0 {
    option routers                10.0.0.1;
    option subnet-mask            255.255.255.0;
    max-lease-time               43200;
    pool {
         range 10.0.0.150 10.0.0.225;
    }
}

# Set name server to appear at a fixed address
host ns {
     next-server ns1.hands-onhistory.com;
    hardware ethernet 00:D0:B3:79:B5:35;
    fixed-address 10.0.0.1;
}
```

In this example, this DHCP server provides IP addresses for client computers on a small LAN. The first line tells the DHCP server not to update DNS records for the local domain based on the IP addresses it assigns. (You can set `ddns-update-style none;` to either `ad-hoc` or `interim` if you have a DNS system that is configured to have your DHCP server update host/address records for the host systems it serves.)

The DHCP server is serving a single LAN, represented by a `10.0.0.0` network address with a `255.255.255.0` netmask. Other data in this file defines what information the DHCP server will hand out to clients on this LAN.

A single server at address `10.0.0.1` is used as the router (or gateway) and DNS server for the LAN. A secondary DNS server is at `10.0.0.2`. To ensure that the first server always gets the fixed address of `10.0.0.1`, a `host` entry is set to the hardware address (`00:D0:B3:79:B5:35`) for the Ethernet card on the host named `ns`. Using the MAC address as shown under `hardware` along with the option `deny unknown-clients;`, you can allow only specified MAC addresses to obtain IP addresses from your DHCP server.

The pool of addresses handed out by this DHCP server is `10.0.0.150` to `10.0.0.225`, as set by the `range` line. Along with the IP address that each client is assigned, the client is also given the associated subnet mask and domain name.

The IP addresses that the DHCP server hands out are leased to each client for a particular time. The `default-lease-time` (set to 21,600 seconds here, or 6 hours) is the time assigned if the client doesn’t request a particular lease period. The `max-lease-time` (43,200 seconds here, or 12 hours) is the highest amount of time the server will assign, if the client requests it. Clients can renew leases, so they don’t have to lose an IP address while they are still using it.

## Expanding the dhcpd.conf file

As I noted earlier, this is a very simple example that works well for a single network of client computers. The following are some examples of ways that you can expand your `dhcpd.conf` file.

- If you have multiple ranges of addresses on the same subnetwork, you can add multiple `range` options to a `subnet` declaration. Here is an example:

```conf
subnet 10.0.0.0 netmask 255.255.255.0 {
  range 10.0.0.10 10.0.0.100;
  range 10.0.0.200 10.0.0.250;
}
```

This example causes the DHCP server to assign IP addresses between the ranges of 10 and 100 and between 200 and 250 on network `10.0.0.0`.

- You can set fixed addresses for particular host computers, also called *address reservations*. In particular, you would want to do this for your server computers so that their addresses don’t change. While you could simply omit the fixed IP addresses from your pool of DHCP assigned addresses, you would lose centralized management of IP configurations. The DHCP reservations allow you to centrally configure all IP address information. One way to do this is based on the Ethernet hardware address of the server’s Ethernet card. All information for that computer can be contained in a `host` definition, such as the following:

```conf
host pine {
  hardware ethernet 00:04:5A:4F:8E:47;
  fixed-address 10.0.0.254;
}
```

Here, when the DHCP server encounters the Ethernet address, the `fixed-address` `10.0.0.254` is assigned to it. It’s a good idea to statically assign server IP addresses. Type `ifconfig -a` on the server computer to see the address of its Ethernet hardware (while the interface is up). Within this `host` definition, you can add other options as well. For example, you could set the location of different routes (`routers` option).

- Many of the options enable you to define the locations of various server types. These options can be set globally or within particular `host` or `subnet` definitions. For example:
