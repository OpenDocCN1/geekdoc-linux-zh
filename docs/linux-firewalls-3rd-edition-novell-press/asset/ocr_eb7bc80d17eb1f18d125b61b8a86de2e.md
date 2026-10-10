```
SIPT -A OUTPUT -0 $INTERNET -p udp \\
-s $IPADDR --sport $TRACEROUTE_SRC_PORTS \\
--dport $TRACEROUTE_DEST_PORTS -j ACCEPT
```

Because **tracroute** is a less secure UDP service and can be used to identify your edge router, map your LAN, or attack other UDP services, allowing incoming **tracroute** isn’t recommended.

# Accessing Your ISP's DHCP Server (UDP Ports 67, 68)

DHCP exchanges, if any, between your site and your ISP’s server will necessarily be local client-to-remote server exchanges. Most often, DHCP clients receive temporary, or semiperma- nent, dynamically allocated IP addresses from a central server that manages the ISP’s customer IP address space. The server also typically provides your local host with other configuration information, such as the network subnet mask; the network MTU; the default, first-hop router addresses; the domain name; and the default TTL.

If you have a dynamically allocated IP address from your ISP, you need to run a DHCP client daemon on your machine. It’s not uncommon for bogus DHCP server messages to fly around your ISP’s local subnet if someone runs the server by accident. For this reason, it’s especially important to filter DHCP messages to limit traffic between your client and your specific ISP DHCP server as much as possible.

Table 4.14 lists the DHCP message type descriptions, as quoted from RFC 2131, “Dynamic Host Configuration Protocol.”

TABLE 4.14
DHCP Message Types

| DHCP MESSAGE | DESCRIPTION |
| :--- | :--- |
| DHCPDISCOVER | Client broadcast to locate available servers |
| DHCPOFFER | Server to client in response to DHCPDISCOVER with offer of configuration parameters |
| DHCPREQUEST | Client message to servers either (a) requesting offered parameters from one server and implicitly declining offers from all others;(b) confirming correct- ness of previously allocated address after, for example, system reboot; or (c) extending the lease on a particular network address |
| DHCPACK | Server to client with configuration parameters, including committed net- work address |
| DHCPNAK | Server to client indicating that client’s notion of network address is incor- rect (for example, client has moved to new subnet) or client’s lease has expired |