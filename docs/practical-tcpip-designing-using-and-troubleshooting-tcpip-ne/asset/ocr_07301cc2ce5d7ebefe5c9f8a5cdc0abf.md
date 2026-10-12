# H. Install your firewall

This is covered in detail in Chapter 24. However, for convenience you might like to record the following settings here or on your network sketch. (The LAN-default-gateway may be the router's internal address, or the firewall's internal address, depending on your firewall model, and whether you're using NAT or not – see Chapter 24 for details.)

| | |
| :--- | :--- |
| **firewall's external interface address** | - . - . - . - |
| **firewall's external interface netmask** | - . - . - . - |
| **firewall's internal interface address** | - . - . - . - |
| **firewall's internal interface netmask** | - . - . - . - |
| **LAN-IP-range** (private if NAT) | - . - . - . - |
| **LAN-netmask** | - . - . - . - |
| **LAN-default-gateway** | - . - . - . - |

If your firewall is NATing, NAT becomes active now, so you have to renumber any test machines (which are behind the firewall) and repeat the tests listed in step F above.

From here on, your network is protected, so anything you install can remain as part of your live network.

# J. Configure your DHCP server if you want to use DHCP

Using DHCP is so easy and has so many advantages that you should certainly use it unless you have a tiny site. If you don't have a router or other device that provides DHCP, you can easily run a DHCP server on a server machine. If you won't be installing that until later, you can use static addressing on your LAN for now and switch to DHCP later with very little effort. Whether you use DHCP or not affects nothing else in your implementation, so do whatever makes life easier for you.

+   - change the PCs on the LAN to use DHCP
+   - repeat the tests from step H above.

# K. Add one or two more PCs to your LAN and test again

Connect one or two more PCs to your LAN and configure them. Then:

+   - check that all PCs on the LAN can contact each other
+   - repeat all the earlier tests (a–f in step F) for the new machines.

This verifies that your LAN is working correctly, that you can connect out to machines on the Internet, and that users on the Internet can connect in to you.