The e-mail or page you will receive will look like the following:

```
rsh:cavu:root@cracker.com as root: cmd='chown root /bin/csh;
chmod 4777 /bin/csh'
```

#  8.10 Using Arpwatch to Catch ARP and
 MAC Attacks

On any Ethernet-based Local Area Network (LAN), at the lowest level packet destinations are specified by the machine's Ethernet card's address, more commonly known as the Media Access Control (MAC) address. When a system wants to send a packet to a particular IP address, it sends out an Address Resolution Protocol (ARP) request saying “Who is IP 10.0.0.27” for example. If everyone is playing fair and is properly configured, the intended system will say “I do and my MAC address is 00:87:72:23:7F:AA. The source system sends the packet to MAC address 00:87:72:23:7F:AA. This protocol was designed over 20 years ago, long before the modern Internet existed, when nobody worried about security and only experienced SysAdmins had administrative access to the systems on a LAN.

Now, anyone can plug a laptop into the network and respond to the ARP requests and thoroughly attack the network. Once a network has grown beyond 10 or so systems, management becomes nontrivial. Even well-intentioned users can use conflicting IP addresses unintentionally, forget to change their laptops' IP addresses to the correct one for the organization, and so on.

> Many networks use Dynamic Host Configuration Protocol (DHCP) or ZeroConf to assign IP addresses automatically, but the use of these programs does not completely prevent IP conflicts. There are many ways that a duplicate IP address could be caused by the DHCP server. The most common is system administrator error. However, if the lease file were to be corrupted or removed, duplicate DHCP leases could be handed out.

The best solution for both accidental and intentional problems is to monitor ARP traffic with Arpwatch. This Open Source program was developed by the U.S. government's Lawrence Berkeley Laboratories and runs on Linux and UNIX. In the spring of 2002, I made some major enhancements to it for better tracking of problems on large networks of