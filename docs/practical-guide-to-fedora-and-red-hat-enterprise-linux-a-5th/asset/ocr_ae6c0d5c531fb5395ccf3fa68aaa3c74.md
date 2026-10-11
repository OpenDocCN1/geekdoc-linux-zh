Wireless networks operate in either ad hoc or infrastructure mode. In ad hoc mode, individual nodes in the network communicate directly with each other. In infrastructure mode, nodes communicate via a WAP (page 597). Infrastructure mode is generally more reliable if the wireless LAN communicates with a wired LAN.
If you do not want to use a WAP, it may be possible to set up a WLAN card so it acts as a WAP; consult the NIC/driver documentation for more information.

# # Configuring the Systems

Once the hardware is in place, each system needs to be configured so that it knows about the NIC that connects it to the network. By default, Fedora uses the Network-Manager daemon (discussed in the next section) to collect information about and to activate the NIC.

The kudzu utility detects and configures new hardware and gives a RHEL system the information it needs about the NIC. The kudzu utility probes the NIC when you install RHEL or the first time you boot the system after you install a NIC. When it prompts you for information, kudzu allows you to specify only one nameserver. It is a good idea to specify at least two or three nameservers; you can use system-config-network to add nameservers.

In addition to information about the NIC, each system needs the following information:

+   - The system's IP address
+   - The netmask (subnet mask) for the system's address (pages 371 and 443)
+   - The IP address of the gateway
+   - The IP addresses of the nameservers (DNS addresses)
+   - The system's hostname (set when you install Fedora/RHEL)

If you set up a DHCP server (page 451) to distribute network configuration information to systems on the LAN, you do not need to specify the preceding information on each system; you just specify that the system is using DHCP to obtain this information. You need to specify this information when you set up the DHCP server.

When you set up a LAN, the IP addresses of the systems on the LAN are generally not made public on the Internet. Some special IP addresses, which are part of the private address space defined by IANA (page 1087), are reserved for private use and are appropriate to use on a LAN (Table 17-1). Unless you have been assigned IP addresses for the systems on the LAN, choose addresses from the private address space.