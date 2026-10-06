# 748 Part V ♦ SUSE Linux in the Enterprise

![](bbox=[0.218, 0.135, 0.858, 0.508])

Figure 30-10: Checking network configuration
Network card setup
Configure your network card here.
Network cards configuration
- Network cards to configure
Available are:
Other (not detected)

Already configured devices:
* Digital EDChip 21041 [Tulip Pass 3]
Configured as eth0 with address 192.168.1.67

Adding a network card:
Choose a network card from the list of detected network cards. If your network card was not autodetected, select Other (not detected) then press Configure.

Editing or deleting:
if you press EDR, an additional dialog in which to change the configuration opens.
Configure...
Back Abort Finish

# Configuring SLOX

WhenLinux has been configured, you move on to the SLOX-specific configuration:

+   1. We will be configuring SLOX as an Internet-facing mail server, talking to an external Domain Name System (DNS) server (Internet lookup capable). With this mind, we will not configure an internal DNS or Samba server because this is not needed for the operation of the mail server and is rarely used in an existing network.

If you want to configure a DNS and Samba server, you need to set the group (or Windows domain name) of the Samba server. For the DNS and Dynamic Host Configuration Protocol (DHCP) server, you do not need to enter any information for the servers. The configuration of Samba, DNS, and DHCP is then handled through the SLOX interface. For more information on Samba, DNS, and DHCP, refer to Chapters 18, 20, and 21.

+   2. To move past the DNS and Samba configuration and to continue on to the LDAP server configuration, click Next. LDAP server configuration (see Figure 30-11) is integral to the configuration of SLOX because all configuration, user, and address functionality is stored here.

> Note