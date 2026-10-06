# CHAPTER 3 Fundamentals of Firewalls

FYI: High-Speed Home or Small Office Connections

With the growing popularity of cable, DSL (Digital Subscriber Line), FIOS (FIOS) is purported to be a Gaelic world that means "knowledge" connections for homes and small offices, where emphasis is placed on securing computer systems in these locations. A general reference to this classification of design is called a Small Office and Home Office (SOHO) facility. Very inexpensive router-based firewalls for your high-speed Internet connection are available. Consumers can also purchase a router that is separate from the DSL or cable router or one that includes the functions of the cable or DSL router with the firewall. The following websites provide more information about these:

+   * Linksys: https://www.linksys.com/
* Home PC Firewall Guide: www.firewallguide.com
* Broadband Guide: www.firewallguide.com/broadband.com

# Types of Firewalls

Packet filtering firewalls are the simplest and often the least expensive type of firewalls. Several other types of firewalls offer their own distinct advantages and disadvantages. The basic types of firewalls are

+   * Packet filtering
* Application gateway
* Circuit level gateway
* Stateful packet inspection

# Packet Filtering Firewall

Packet filtering firewall is the most basic type of firewall. In a packet filtering firewall, each incoming packet is examined. Only those packets that match the criteria you set are allowed through. Many operating systems, such as Windows clients (as with Windows 8 and 10) and many Linux distributions, include basic packet filtering software with the operating system. Packet filtering firewalls are also referred to as screening firewalls. They can filter packets based on size, protocol used, source IP address, and other parameters. Some routers offer this type of firewall protection in addition to their normal routing functions.

Packet filtering firewalls work by examining a packet's source address, destination address, source port, destination port, and protocol type. Based on these factors and the rules that the firewall has been configured to use, they either allow or deny passage to the packet. These firewalls are very easy to