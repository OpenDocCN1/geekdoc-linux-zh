86

Chapter 7 · DHCP and DNS

There is a workaround, however, though it defeats the purpose of DDNS by requiring a manual configuration of the DHCP server. You can create a reservation on the DHCP server for the HP-UX client and then specify Option 12, the host name, as part of the reservation. Therefore, when the HP- client requests a DHCP lease, the server will respond with a lease containing the host name, along with the DNS domain name, to update the DDNS server. While this process works for DDNS, it fails for DHCP, since you have to make reservations for each client that does not support either Option 12 or 81 in its DHCP messages. Until HP-UX supports one of these options, having an HP-UX client of a Windows 2000 server is a bit problematic.

# 7.2.12 Windows 2000 DHCP Client and HP-UX DHCP Server

A Windows 2000 DHCP client can get all the networking configuration it needs from an HP-UX 11 DHCP server. This information includes not only the usual stuff like IP address, DNS server, gateway, and DNS domain name, but also NetBIOS name server (Option 44), NetBIOS node type (Option 46), and NetBIOS Scope (Option 47).

However, the HP-UX DHCP server does not perform any update requests to DDNS, be it Windows 2000 DNS or B version 8. To ensure that this happens, you must register the connection's addresses in DNS box on the DNS tab of the Advanced TCP/IP settings box. (See Figure 7–1.) The Windows 2000 client will then follow the dynamic update process:

+   1. Query the local name server for the primary name server and the update zone.
2. Using the information in the local name server's response, send a dynamic update request to the authoritative primary server for the zone.

If you want the connection-specific DNS suffix to be registered in DDNS, you must also check the Use connection's DNS suffix in DNS registration box. Otherwise, the client will use the primary suffix.

# 7.2.1.3 DDNS on HP-UX

To upgrade BIND on HP-UX to version 8.1.2 in order to implement DDNS. (As of this writing, this was the latest supported version of BIND on HP-UX.) Once you do, you can enable dynamic updates by editing the /etc/named.conf file, the BIND configuration file. This file lists statements ending in semicolons; some statements contain a block of substatements or options. You need to add an allow-update option to the zone statement. The zone statement defines a zone in the configuration file. The allow-update option specifies which hosts are allowed to send update requests to DDNS (The default is to deny updates from all hosts.) For more information, see “ISC BIND Documentation” page at http://www.isc.org/products/BIND/docs/index.html.

The syntax of this option is allow-update { address_match_list }, where address_match_list can be an IP address (dotted-notation), an IP prefix (the “/ notation), or the name of an address match list premi