plaintext records. SNMP version 2 (called SNMPv2) implemented a basic level of security and provided for the bulk transmission of monitoring data to help reduce the network traffic required to monitor devices. The current version (SNMPv3) utilizes both strong authentication and data encryption capabilities and provides a more streamlined management system.

The most popular SNMP software package in Linux is the open source net-snmp package. This package has SNMPv3 compatibility, allowing you to securely monitor all aspects of a Linux server remotely.

# ## Time

For many network applications to work correctly, both servers and clients need to have their internal clocks coordinated with the same time. The Network Time Protocol (NTP) accomplishes this. It allows servers and clients to synchronize on the same time source across multiple networks, adding or subtracting fractions of a second as needed to stay in sync.

For Linux systems, the ntpd program synchronizes a Linux system with remote NTP servers on the Internet. It’s common to have a single Linux server use ntpd to synchronize with a remote time standard server and then have all other servers and clients on the local network sync their times to the local Linux server.

# # Implementing Security

These days, security is at the top of every system administrator’s list of worries. With a seemingly endless supply of people trying to break into servers, implementing security is a vital role for every Linux administrator.

Fortunately, Linux provides several layers of security that you can implement in your Linux server environment. The following sections walk through the server software packages that you may run into as you implement security in your Linux servers.

# ## Authentication Server

The core security for Linux servers is the standard userid and password assigned to each individual user on the system and stored in either the /etc/passwd (on non-secure legacy systems) or the /etc/shadow file. Each Linux server maintains its own list of valid user accounts that have access on that server.

For a large network environment where users may have to access resources on multiple Linux servers, trying to remember multiple userids and passwords can be a challenge. Fortunately, there are a few different methods for sharing user account databases across multiple Linux servers on a network.