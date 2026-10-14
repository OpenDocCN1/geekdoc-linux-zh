TIP
SANS also coordinates with the FBI to provide a Top 20 list of the most widely used strategies for attacking computer systems. You can review this list to make certain that your systems are protected against known security threats.

The information on the SANS Web site is continually updated and includes a number of Linux-specific security resources. Beyond this, SANS maintains a highly regarded hands-on certification program for security professionals: the Global Information Assurance Certification (GIAC) program. Related to this effort, SANS focuses a great deal of energy on providing technical conferences in cities around the world. These are amazing conferences, where top security experts teach hands-on courses to network administrators who face security threats each day.

TIP
Other useful Web sites that contain computer security information include www.securityfocus.com and www.securitymanagement.com.

# USING NETWORK SERVICES

In several previous chapters you have learned about many aspects of networking. In this section, you are introduced to a number of different network services that typically run on Linux. Most of these are installed by default and are controlled using a script in the /etc/rc.d/init.d directory, or using the service command (as discussed in Chapter 9). Although the level of detail provided in this section for each of these services is minimal, it should be enough to acquaint you with the service, start it up, and explore how it operates using the commands and documentation referenced. After reading this section, you should expect to both experiment and study before you feel ready to implement these services on a production server—each of these topics deserves a book of its own.

# Using NetFilter for Firewalls

A firewall is a hardware device or software program that prevents unintended network access. A packet filter is a firewall that performs this function by examining the information stored in each packet and deciding how to process that packet based on rules established as part of the firewall. The Linux kernel includes the ability to filter network packets. The packet-filtering feature in older Linux kernels was called IP chains, and you can still see information about this feature in various kinds of Linux documentation.

The latest Linux kernels use a feature called NetFilter, which includes an enhancement of the IP chains system called IP tables. Both IP chains and IP tables let you define a list of rules (a chain or a table, respectively). Each network packet is compared against the rules that you define as the kernel decides what to do with it: discard it, forward it to another system, change information within the packet and pass it on, and so on. Although the NetFilter