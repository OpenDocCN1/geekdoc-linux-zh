# 422 Linux Administration: A Beginner's Guide

The Domain Name System (DNS) provides a way to map or translate an unfriendly numerical IP address into a people-friendly format. Although this translation isn't mandatory, it does make the network much more useful and easy to work with humans.

At inception of the Internet in the 1970s, IP address-name mapping was done through the maintenance of a hosts.txt file that was distributed via FTP to all the machines on the Internet. As the number of hosts grew (starting in the early 1980s), it soon clear that a single person maintaining a single file of all of those hosts was not a scalable way of managing the association of IP addresses to hostnames. To solve this problem, a distributed system was devised in which each site would be authoritative, and that each site had host address would be kept in a master table that could be queried by all other sites. This is the essence of DNS.

If the information wasn't decentralized, as it is now, one choice would be to have a central site maintaining a list of all hosts (numbering in the tens of millions) and having to update those hostnames thousands of times a day—one site might need to maintain a private DNS server because its firewall requires that local area network (LAN) IP addresses not be visible to outside networks, yet the hosts in the LAN must be able to find hosts on the Internet. If you're sturned by the prospect of having to manage this for every host on the Internet, you're getting the picture.

We will discuss DNS in depth, so you'll have what to configure and deploy your own DNS servers for whatever your needs might be.

> NOTE In this chapter, you will use the terms "DNS server" and "name server" used interchangeably. Technically, "name server" is a little ambiguous because it can apply to any number of naming schemes that resolve a name to a number and vice versa. In the context of this chapter, however, "name server" will always mean a DNS server unless otherwise stated.

# The Hosts File

Not all sites run their own DNS servers ... and not all sites need their own DNS servers! In sufficiently small sites with no Internet connectivity, it's reasonable for each host to keep its own copy of a table matching all of the hostnames on the local network with their corresponding IP addresses. In most Linux and UNIX systems, this table is stored in the /etc/hosts file.