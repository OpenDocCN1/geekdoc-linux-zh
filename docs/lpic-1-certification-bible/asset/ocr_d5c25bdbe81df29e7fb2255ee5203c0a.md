*pppd reads options from the files /etc/ppp/options, ~/.ppprc, and /etc/ppp/options.tname (in that order) before processing the options on the command line. This allows the options to be configured in one of these scripts instead of entering them at the command line.*

The command to initiate a PPP connection using an ISDN line is as follows:

```
```
# pppd connect 'chat -f /etc/ppp/ppp_isdn.chat' holdoff 60 /dev/isdn 64000
```
```

# # Key Point Summary

This chapter covers many important concepts and utilities used to provide network connectivity on a Linux system. Some of the most important items covered in this chapter include the following:

+   - TCP/IP addresses are used to uniquely identify each network interface on the network. These addresses can be viewed using binary or decimal format.

+   - The three most commonly used network classes and matching network masks are as follows:
+     - Class A: 1.0.0.0–126.0.0.0, with the mask 255.0.0.0
+     - Class B: 128.0.0.0–191.0.0.0, with the mask 255.255.0.0
+     - Class C: 192.0.0.0–223.0.0.0, with the mask 255.255.255.0

+   - The TCP/IP protocol suite comprises the following primary protocols: IP, ARP, ICMP, TCP, and UDP. IP is responsible for the delivery of datagrams across the network. ARP provides IP address-to-hardware address mapping and translation, and ICMP reports errors in the delivery of packets. TCP is a connection-oriented protocol that provides reliable transmission of data using sessions. UDP provides connectionless transmissions with less overhead than TCP.

+   - TCP and UDP make use of ports and sockets to manage multiple connections to a variety of applications simultaneously. Applications are mapped to specific ports using the /etc/services file.

+   - The FTP application allows for file transfer from remote systems, while Telnet allows remote access to a system’s shell.

+   - The host command allows you to discover IP or hostname information for the specified system. The whois command provides domain, name server, and contact information for the specified domain. The finger utility can be used to discover information about a specific user on a system.