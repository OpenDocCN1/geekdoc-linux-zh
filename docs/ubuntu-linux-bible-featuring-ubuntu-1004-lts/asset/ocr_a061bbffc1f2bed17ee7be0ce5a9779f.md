# Setting Up a DNS Server

As I mentioned in Chapter 31, "Setting Up a DHCP Server," a long time ago when even I was young, the Internet (or the ARPANET as it was called in those days) was a small place with a limited number of hosts, all of which had fixed IP addresses. The mappings between those IP addresses and the actual names of those hosts were maintained in a central text file. Yes, that's, a single text file. Everyone shared this text file (HOSTS.TXT) with everyone else retrieving it from the Stanford Research Institute's Network Center (the true NIC) every so often, and adding their own modifications for any private local hosts and networks. However, as the ARPANET grew and more and more hosts became networked, maintaining all of this information in a single file became not impractical, but silly.

Not only was this file long (and getting longer), but also its format was specified by convention rather than explicit delete; luckily, the Internet/ARPANET was created by smart people, so many improvements to the model occurred in the early 1980s. For example, in March of 1982, the hosts table definition was updated with the Department of Defense Host Table Specification (RFC 810). Shortly thereafter, a server function to provide individual hostname/address translations was described in Request For Comment 811, which introduced the idea of dynamically providing and maintaining host information. RFC 819, "The Domain Naming Convention for Internet User Applications," woke everyone up, and RFC 830, "A Distributed System for Internet Name Service," suggested the one true concept of a distributed system of name servers, each serving its local domain. From 1982 to 1983 was a busy time for the fundamental concepts that we all take for granted today (and may not be aware of).

# IN THIS CHAPTER

+   - Overview DNS and BIND

+   - Overviewing BIND configuration files

+   - Creating zone files

+   - Creating reverse lookup files

+   - Troubleshooting DNS