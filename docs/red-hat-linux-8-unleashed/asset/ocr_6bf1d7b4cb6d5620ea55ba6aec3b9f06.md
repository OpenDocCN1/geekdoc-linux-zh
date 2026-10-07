# CHAPTER 13 Network Connectivity

NETWORKING=yes
HOSTNAME="myhost.mydomain.com"
GATEWAY="192.112.50.99"
GATEWAYDEV=""
FORWARD_IPV4="no"

The only additional optional entry to /etc/sysconfig/network is for NIS machines and would look like this:

NISDOMAIN=rebel

The FORWARD_IPV4 value determines whether the host forwards IP packets. This would be for routers. This file is modified when any of the listed information changes.

# Using Red Linux Graphical Configuration Tools

As mentioned earlier, if you're new to networking or still becoming proficient with the command line, the graphical configuration tool is your best method for configuring new hardware in Red Hat Linux. Most graphical tools, redhat-config-network allows you to fill in the blanks; press the buttons, and the tool will modify the required files and issue the proper commands. Remember, you must boot to run redhat-config-network.

There are two ways to start redhat-config-network: from the command line of an X11 terminal window with the command /sbin/redhat-config-network or by clicking the Network Configuration item from GNOME or KDE desktop menu. In either case, you'll be prompted to enter the root password.

Once started, redhat-config-network might ask if you'd like to create a new device. If you've installed Red Hat Linux on a computer with an existing network card, however, the screen in Figure 13.1 appears after you start redhat-config-network.

Click the DNS tab to configure your system's DNS settings, hostname, or DNS search path. Click the Hosts tab, and then click the Add or Edit button to create or edit an entry in your system's /etc/hosts file, to add the IP addresses, hostnames, and aliases of hosts on your network (see Figure 13.2).

Click on Devices tab, and then click Add or select an existing setting and click Edit to automatically or manually set up an Ethernet device. Figure 13.3 shows the Ethernet Device dialog box with all necessary information in place. Choose how your card will get its configuration, manually, from Dynamic Host Control Protocol (see the next section) or from Bootp. Just fill in the blanks as needed.

> NOTE

Bootp is the initial protocol that DHCP was built on, and it has mostly been replaced by DHCP.