With IP masquerading enabled, your Red Hat Linux PC acts as a stand-in for any of the other systems on the Ethernet LAN. As with the router setup, the Red Hat Linux PC is designated as the gateway for the Ethernet LAN. However, masquerading involves more than simply forwarding IP packets back and forth between the LAN and the Internet.

When the Red Hat Linux PC masquerades as another system on the LAN, it modifies outgoing packets so that they always appear to originate from the Red Hat Linux PC. When a response to one of the outgoing packets is received, the Red Hat Linux PC performs the reverse task — it modifies the packets so that they appear to come from the Internet directly to the system that sends the outgoing packet. The end result is that each system on the Ethernet LAN appears to have full access to the Internet, even though the Ethernet LAN uses a non-unique private IP address.

To enable and use IP masquerading, perform the following steps:

+   1. Make sure that the Linux kernel — the core operating system — supports IP firewall chains. This should be true for the version of Red Hat Linux you install from the companion CD-ROMs. If the file `/proc/net/ip_fwchains` exists, then the kernel supports IP firewall chains. (Type `ls /proc/net/ip_fwchains` to verify that the file exists.)
+   2. Make sure the Red Hat Linux PC has an Internet connection and a network connection to your LAN. Typically, the Linux PC has two network interfaces — an Ethernet card for the LAN and a dial-up PPP connection to the Internet (through an ISP).
+   3. Make sure that all other systems on your LAN use the Linux PC as the default gateway for TCP/IP networking. Use the same ISP-provided DNS addresses on all systems.
+   4. Enable IP forwarding in the kernel by typing the following command:
+   `echo "1" > /proc/sys/net/ipv4/ip_forward`
+   This is necessary because IP forwarding is disabled by default. To ensure that IP forwarding is enabled when you reboot your system, place this command in the `/etc/rc.d/rc.local` file. In Red Hat Linux, you can achieve the same result by changing the line `FORWARD_IPV4=false` to `FORWARD_IPV4=true` in the `/etc/sysconfig/network` file.
+   5. Run `/sbin/ipchains` — the IPCHAINS firewall administration program — to set up the rules that enable the Linux PC to masquerade for your LAN. For example, to enable masquerading for a LAN via the Linux PC's `ppp0` network interface, you can use the following commands:
+   `/sbin/ipchains -P forward DENY`
+   `/sbin/ipchains -A forward -i ppp0 -j MASQ`