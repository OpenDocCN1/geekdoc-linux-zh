/var/lib/dhcp/dhclient.leases configuration file. As the number of leases may be large, this file is recreated from time-to-time to ensure a manageable size.

# Configuring a Wireless Interface

The use of wireless network cards has grown rapidly over the last few years due to the increase in speed of the wireless infrastructures. The configuration of a wireless interface is very similar to that of a wired interface. To display the status of all the wireless interfaces on a system, iwconfig is used with no parameters or the iwlist command, which is found in /usr/sbin. The wireless statistics are obtained from the /proc/net/wireless file.

To set up a wireless NIC, the main parameters to be used are given below:

+   ESSID is used to set the network name to enable the user to roam across a number of access points.

+   mode will need to be set depending on the network topology. The common parameters are managed for a network of many access points, ad hoc for a point-to-point connection, and master if the device will act as access point.

+   key/enc is used to set the current encryption key, and is entered in hex notation in the form XXXX-XXXX-XXXX-XXXX or as an ASCII string with the s : prefix.

# Network Configuration Files

There are a number of network configuration files in the systems that are modified automatically or manually. The files can have comments embedded in them using the # symbol as per normal, and it is advisable to add meaningful comments if these files are modified manually.

# Hosts File, /etc/hosts

The hosts file maps actual IP addresses to hostnames. For large networks, this is usually undertaken by using DNS, as the maintenance involved in keeping hosts files current is usually large. The hosts file will contain both IPv4 and IPv6 addresses. Often, it is useful to add a small number of frequently used hosts into the hosts file to reduce the load on the network and name servers.

# Services, /etc/services

The services file maps port numbers to services. A port is specific to an application and is the communication endpoint used by the transport layer protocols in the IP suite. Applications will use these port numbers to ensure that the sending and receiving systems understand which application the