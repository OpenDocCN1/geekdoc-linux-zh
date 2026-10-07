:lp|/usr/share/printconf/util/smbprint:\

:lpd-bounce=true:

:if=/usr/share/printconf/util/mf_wrapper:

![](bbox=[0.288, 0.175, 0.712, 0.413])

FIGURE 12.11 Create a shared remote printer using required information for Windows.

In this example, you can see that an SMB printing filter (smbprint) is used in the lp: field.

# Network-Attached Printer Configuration and Printing

Red Hat Linux supports other methods of remote printing, such as using a Novell Network-based print queue or using a printer attached directly to your network with an HP JetDirect adapter. Some manufacturers offer even Linux-specific drivers and help. For example, HP/Compa provides graphical printer configuration tools and software drivers for earlier versions of Red Hat Linux at http://h20000.www2.hp.com/bizsupport/index.jsp.

You can set up network-attached printing quickly and easily using Red Hat Linux. For example, GEARNET's PS101 print server adapter works well with Linux. This tiny device (a self-hosted print server) is an adapter that directly attaches to a Centronics jack, and eliminates the use of a parallel-port cable. The PS101 offers a single 10Mbps Ethernet jack, and after initial configuration and assignment of a static IP address, can be used to print to any supported printer by Red Hat Linux.

A JetDirect- or UNIX-based configuration using redhat-config-printer can be used to allow you to print to the device from your Red Hat system. To see any open ports or services on the device, use the nmap command with the print server adapter's IP address like:

```
$ nmap 192.168.2.52
```

Starting nmap V. 2.54BETA22 ( ..insecure.org/nmap/ )

Interesting ports on (192.168.2.52):