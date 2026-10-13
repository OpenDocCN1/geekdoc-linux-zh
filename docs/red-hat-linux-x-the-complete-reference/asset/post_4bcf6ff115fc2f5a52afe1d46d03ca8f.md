
```code
key myserver {
  algorithm HMAC-MD5;
  secret "CNQAfBBLnvWUSH8hRqq/WA==";
};
```

The key's name can then be used to reference the key in other named statements, such as **allow-update** statements.

```code
allow-update myserver;
```

The DNS server or DHCP server with which you are setting up communication will also have to have the same key. See the earlier section "Dynamic Update: DHCP and Journal Files" and Chapter 35 for more information on DHCP and TSIG. For communication between two DNS servers, each would have to have a server statement specifying the shared key. In the following example, the named.conf file for the DNS server on 192.168.0.1 would have to have the following server statement to communicate with the DNS server on 10.0.0.1, using the shared myserver key. The named.conf file on the 10.0.0.1 DNS server would have to have a corresponding server statement for the 192.168.0.1 server.

```code
server 10.0.0.1 { keys {myserver;}; };
```

## Split DNS: Views

BIND 9.x allows you to divide DNS space into internal and external views. This organization into separate views is referred to as split DNS. Such a configuration is helpful to manage a local network that is connected to a larger network, such as the Internet. Your internal view would include DNS information on hosts in the local network, whereas an external view would show only the part of the DNS space that is accessible to other networks. DNS views are often used when you have a local network that you want to protect from a larger network such as the Internet. In effect, you protect DNS information for hosts on a local network from a larger external network such as the Internet.

### Internal and External Views

To implement a split DNS space, you need to set up different DNS servers for the internal and external views. The internal DNS servers will hold DNS information about local hosts. The external DNS server maintains connections to the Internet through a gateway as well as manages DNS information about any local hosts that allow external access, such as FTP or Web sites. The gateways and Internet-accessible sites make up the external view of hosts on the network. The internal servers handle all queries to the local hosts or subdomains. Queries to external hosts such as Internet sites are sent to the external servers, which then forward them on to the Internet. Queries sent to those local hosts that operate external servers such as Internet FTP and Web sites are sent to the external DNS servers for processing. Mail sent to local hosts from the Internet is handled first by the external servers, which then forward messages on to the internal servers. With a split DNS configuration, local hosts can access other local hosts, Internet sites, and local hosts maintaining Internet servers. Internet users, on the other hand, can access only those hosts open to the Internet (served by external servers) such as those with Internet servers like FTP and HTTP. Internet users can, however, send mail messages to any of the local hosts, internal and external.

You can also use DNS views to manage connections between a private network that may use only one Internet address to connect its hosts to the Internet. In this case, the internal view holds the private addresses (192.168...), and the external view connects a gateway host with an Internet address to the Internet. This adds another level of security, providing a result similar to IP masquerading (see Chapter 38).

### Configuring Views

DNS views are configured with allow statements such as allow-query and allow-transfer. With these statements, you can specify the hosts that a zone can send and receive queries and transfers to and from. For example, the internal zone could accept queries from other local hosts, but not from local hosts with external access such as Internet servers. The local Internet servers, though, can accept queries from the local hosts. All Internet queries are forwarded to the gateway. In the external configuration, the local Internet servers can accept queries from anywhere. The gateways receive queries from both the local hosts and the local Internet servers. In the following example, a network of three internal hosts and one external host is set up into a split view. There are two DNS servers: one for the internal network and one for external access, based on the external host. In reality these make up one network but they are split into two views. The internal view is known as mygolf.com, and the external as greatgolf.com. In each configuration, the internal hosts are designated in ACL labeled internals, and the external host is designated in ACL labeled externals. Should you want to designate an entire IP address range as internal, you could simply use the network address, as in 192.168.0.0/24. In the options section, allow-query, allow-recursion, and allow-transfers restrict access within the network.

### Split View Example

The following example shows only the configuration entries needed to implement an internal view. In the mygolf.com zone, queries and transfers are allowed only among internal hosts. The global allow-recursion option allows recursion among internals.

```code
acl internals { 192.168.0.1; 192.168.0.2; 192.168.0.3; };
acl externals {10.0.0.1;};
options {
    forward only;
    forwarders {10.0.0.1;}; // forward to external servers
    allow-transfer { none; }; // allow-transfer to no one by default
    allow-query { internals; externals; };// restrict query access
    allow-recursion { internals; }; // restrict recursion to internals
}
zone "mygolf.com" {
    type master;
    file "mygolf";
    forwarders { };
    allow-query { internals; };
    allow-transfer { internals; }
};
```

In the configuration for the external DNS server, the same ACLs are set up for internals and externals. In the options statement, recursion is now allowed for both externals and internals. In the mygolf.com zone, queries are allowed from anywhere, and recursion is allowed for externals and internals. Transfers are not allowed at all.

### External DNS server

```code
acl internals { 192.168.0.1; 192.168.0.2; 192.168.0.3; };
acl externals {10.0.0.1;};
options {
    allow-transfer { none; }; // allow-transfer to no one
    allow-query { internals; externals; };// restrict query access
    allow-recursion { internals; externals }; // restrict recursion
};
zone "greatgolf.com" {
    type master;
    file "greatgolf";
    allow-query { any; };
    allow-transfer { internals; externals; };
};
```

![](img/32a48d8db4c23e6e2eb70d1e5034c976_857_0.png)

# Chapter 35: DHCP Server

## Overview

Many networks now provide the DHCP service that automatically provides network configuration for all connected hosts. They use a protocol called DHCP (Dynamic Host Configuration Protocol). With the DHCP protocol an administrator can use a pool of IP addresses from which it can assign an IP address to a host as needed. The protocol can also be used to provide all necessary network connection information such as the gateway address for the network or the netmask. Instead of having to configure each host separately, network configuration can be handled by a central DHCP server. The length of time that an address can be used can be controlled by means of leases, making effective use of available addresses. If your network is configuring your system with DHCP, you will not have to configure it manually. All necessary information will be automatically entered into your network configuration files.

DHCP provides configuration information to systems connected to a TCP/IP network, whether the Internet or an intranet. The machines on the network operate as DHCP clients, obtaining their network configuration information from a DHCP server on their network. A machine on the network runs a DHCP client daemon that automatically downloads its network configuration information from its network's DHCP server. The information includes its IP address, along with the network's name server, gateway, and proxy addresses, including the netmask. Nothing has to be configured manually on the local system. This has the added advantage of centralizing control over network configuration for the different systems on the network. A network administrator can manage the network configurations for all the systems on the network from the DHCP server.

> **Note** DHCP is based on the BOOTP protocol developed for diskless workstations. Check DHCP documentation for options specific to machines designed to work with BOOTP.

A DHCP server also supports several methods for IP address allocation: automatic, dynamic, and manual. Automatic allocation assigns a permanent IP address for a host. Manual allocation assigns an IP address designated by the network administrator. With dynamic allocation, a DHCP server can allocate an IP address to a host on the network only when the host actually needs to use it. Dynamic allocation takes addresses from a pool of IP addresses that hosts can use when needed and release when they are finished.

The current version of DHCP now supports the DHCP failover protocol in which two DHCP servers support the same address pool. Should one fail, the other can continue to provide DHCP services for a network. Primary and secondary servers in this scheme are designated with the primary and secondary statements.

A variety of DHCP servers and clients are available for different operating systems. For Linux, you can obtain DHCP software from the Internet Software Consortium (ISC) at www.isc.org. The software package includes a DHCP server, a client, and a relay agent. Linux includes a DHCP server and client. The DHCP client is called dhcpc, and the server is called dhcpd. The network information a DHCP client downloads is kept in its own network configuration files in the /etc/dhcpcd directory. For example, here you can find a resolv.conf file for your network's name servers.
