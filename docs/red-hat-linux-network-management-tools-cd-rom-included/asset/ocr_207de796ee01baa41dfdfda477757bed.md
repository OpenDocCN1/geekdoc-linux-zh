are 204.127.129.1, 204.127.160.1, and 10.0.2.278. These entries tells the system which name server should be queried and in what order when hostname resolution is used. The search field tells the system which additional domains should be appended to the host-name when querying one of the defined name servers. A name server will be responsible for supporting one or more domains to which specific hosts have been associated. In this case, scarecats belongs to the home.com domain, but the system can also query additional hosts that belong to other domains.

The DNS information is stored in the /etc/resolv.conf configuration file, and a change made to the hostname automatically updates these files. Note that any previous information saved in the configuration files will be overwritten with the contents of the fields each time they are saved.

# Maintain Host Database

The Hosts button maintains entries with the /etc/hosts file, and selecting this button displays the contents of this file for the current view.

Changes are made only to the local hosts file. If you are running NIS or DNS, changes made to this file will not affect either of these resolution services.

Note

This system file contains hostname-to-IP address mappings and consists of up to three fields: IP, Name, and Nicknames. The IP address represents the unique address for the designated host. It is not something you just pull out of a hat. This address is specifically assigned to a system or, in the case of using dynamic IP allocation, assigned by a server for the specific host to obtain when the host is booted. Normally, if you are running NIS or DNS, you won’t need this file. The bottom line is that all IP addresses assigned to a network must be unique in order for the TCP/IP protocols to function correctly.

Figure 10.4 shows a sample set of hostnames already defined within the local system. These entries only represent mappings between the IP address of the node and some hostname designa-tion. The hostname is strictly for human consumption. The names