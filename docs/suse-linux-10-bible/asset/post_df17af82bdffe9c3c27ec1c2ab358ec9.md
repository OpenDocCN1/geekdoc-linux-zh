
# page_log

The file page_log shows the user and the job name, as well as the number of pages printed. Each page printed shows in the file as a serial number against the job number. By analyzing the page log you can do user accounting. There are a number of tools available for this, including PyKota (www.librelogiel.com/software/PyKota).

# error_log

This file is not really so much an error log as a place where CUPS shows everything about its activity. It is useful for debugging problems because CUPS is doing in the background, for example, which filters are being used to print and so on.

# Other Tools

There are some additional tools (not part of the CUPS package) that are useful for printing.

# kprinter

The KDE interface includes the kprinter tool, which handles printing from all KDE applications. You can set other programs to print via kprinter, too. It has the ability to manage (among other things) paper sizes and printing multiple pages to a single physical page.

# xpp

xpp is the X Printing Panel, a graphical application similar in conception to kprinter, independent of KDE. You can use it to browse for print files, print print queues to send them to, and choose various options appearing the output, the number of copies, and so on.

# gtklp

The gtklp package provides the gtklp graphical printing tool. This tool is similar in functionality to xpp but has a cleaner interface. It allows, among other things, scaling and color adjustment when printing image files.

# Documentation

As is always the case with SUSE Linux, you can find a great deal of documentation to support you as you set up your printing, both locally and on your networks.

# CUPS Online Documentation

The CUPS documentation is installed on the system and can be viewed through the CUPS web interface locally at http://localhost:631/documentation.html or on the CUPS web site at http://www.cups.org/documentation.php. The commands lp, lpr, lpadmin, lpoptions, lpstat, lpg and lprm or other CUPS commands all have man pages.

# The CUPS Book

There is an official CUPS book: CUPS: Common UNIX Printing System by Michael Sweet (Sams). The table of contents is at http://www.cups.org/book/index.php.

# SUSE Printing Documentation

You can find good many articles on printing on the SUSE support database, fully grouped together into a category: http://portal.suse.com/sdb/en/categories/Printing.html.

The SUSE Professional Administration guide has a chapter on Printer Administration.

# IPP Documentation

You can find more information about IPP on the Printer Working Group's site at http://www.pwg.org/ipp/. This includes links to the relevant RFC documents.

CUPS and the SUSE YaST printer module make setting up printing relatively easy CUPS has far more capabilities than can be covered here. If you intend to use CUPS in a large networked environment, you should read the full documentation to find out, in particular about such features as page and job documentation.

# Configuring and Using DHCP Services

## In This Chapter

- DHCP overview
- Configuring DHCP servers in YaST
- Using DHCP clients

Today's networks are more complex than ever before. In addition to traditional requirements that each user's desktop system be connected to the network, many other devices such as printers, fax machines, laptop and notebook computers, and personal digital assistants (PDAs) now require network connections. Because today's networks typically use numerous IP addresses, system administrators must manage the set of IP addresses to place them more effectively within an enterprise and on specific network segments.

Devices like PDAs and notebooks, laptops, and other portable computers bring special requirements to network administration, because they are not always connected to the network and almost always move from place to place. Permanently allocating IP addresses to each PDA and portable computer basically wastes IP addresses when the systems are not connected to the network and may not be possible in a network environment with many different subnets and associated ranges of IP addresses. For example, if your office and main conference room are on different subnets, you cannot simply move your laptop from one location to another, plug it in, and transparently reconnect to the network.

To allocate and manage IP addresses more efficiently, and enable more flexible network configuration in general, today's networks use a variety of protocols for dynamically obtaining and managing IP addresses and associated network information. This chapter discusses the Dynamic Host Configuration Protocol (DHCP), which is the most common and popular dynamic networking configuration mechanism used.

# What Is DHCP?

DHCP is the latest in a long line of protocols to provide an IP address and related information to devices that cannot or are designed not to store such information as part of their configuration. Some devices do not have non-transient memory in which an IP address be stored, which means the device must request an IP address each it boots. In devices that have writable storage as Flash or NVRAM that can preserve configuration across reboots, storing an IP address is a common decision which provides flexibility in network device configurations. Devices that are designed to dynamically request configuration information each time they retain permanent knowledge of their network environment, which can therefore be flexibly reconfigured without any need to reconfigure the network device except by rebooting.

The oldest of network protocols is the Reverse Address Resolution Protocol (RARP). The processes that serve RARP requests, known as RARP daemons, return an IP address based on a configuration file that provides an explicit mapping between a network device's Media Access Control (MAC) address and a specific IP address. A MAC address is a 12-digit hexadecimal number that is stored in the network device and is usually expressed in colon-separated pairs such as MM:MM:MM:SS:SS:SS, where the digits represented by M identify the manufacturer and the digits represented by S specify the serial number to that device by the manufacturer.

RARP daemons can provide only an IP address to a network device. After an IP address has been assigned, network devices that use RARP typically also contain hard-coded instructions in their boot sequence that retrieve mandatory configuration information, such as a boot image, through a simple download protocol such as the Trivial File Transfer Protocol (TFTP). Because the mapping between MAC and IP addresses is flexible, the name of the file containing configuration or boot information must be based on the MAC address, because that is the only non-transient information that is available about the device.

To provide flexibility during the boot process for network devices, the Bootstrap Protocol (BOOT) was introduced as a next-generation boot protocol. BOOT is more advanced than RARP because it enables a network device to retrieve both its IP address and the name of a file to download (usually referred to as a boot image). While this provides additional flexibility, standard BOOT daemons still typically use a configuration file.

The need to maintain a static mapping between MAC and addresses has three main shortcomings:

- It limits the number of devices that can use BOOTP daemon as a limited number of IP addresses are available.
- Predefined IP addresses limit BOOTP devices to specific network segments, the subnet address must be pre-defined.
- Even if different network segments run their own BOOTP daemons, BOOTP requests are invoked only at boot time, which requires rebooting whenever they move across segment boundaries.

DHCP was developed to provide the flexibility required in modern environments, which typically contain multiple subsets and large numbers of devices. DHCP is a client/server protocol that is much more powerful and flexible than IP: DHCP does not require a predefined mapping between MAC and addresses; it delivers an IP address to any authorized network device that requests it. DHCP maintains a pool of available IP addresses that are leased to DHCP-aware devices (which are typically referred to as a DHCP server) for a period of time. When the lease expires, the DHCP client can renew the lease to continue using that IP address. If it is no longer present, the associated IP address is returned to the pool of addresses that are available for assignment.

In addition to this increased flexibility in IP address assignment, DHCP delivers a much wider range of network configuration information than previous boot protocols. DHCP servers can provide DHCP clients with an IP address, host and domain name information, network gateway and other routing information, the address(es) of DNS servers, and so on. DHCP servers provide compatibility with BOOTP daemons and can serve BOOTP requests, although they can only deliver the range of information supported by BOOTP.

DHCP is both a boot and runtime protocol, meaning that network devices can change their IP addresses after they have booted and are running. To do this, they must run a DHCP client process that supports dynamic network reconfiguration. The interaction between a DHCP client and a DHCP server is as follows:

- An unconfigured client sends out a DHCP discover packet to the network to see if a DHCP server exists that can answer a request for configuration information.
- If a server does exist, it sends a response (using the client's MAC address) saying that it can help the client out of a sticky situation with a DHCP offer. If a server does not reply with a DHCP offer, the client will retransmit a DHCP discovery to try and contact a DHCP server.
