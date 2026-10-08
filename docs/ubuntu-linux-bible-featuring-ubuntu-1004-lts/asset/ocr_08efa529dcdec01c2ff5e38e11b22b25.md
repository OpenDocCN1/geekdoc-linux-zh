# Setting Up a DHCP Server

Long time ago even when I was young, the Internet (or the ARPANET as it was called in those days) was a small place with limited number of hosts, all of which had fixed IP addresses and names that were maintained in a file that everyone shared with everyone else, and then added their own local modifications for any private, hosts and networks. However, as the ARPANET grew and more and more hosts became networked, maintaining all of this information in a single file became not only impractical, but also silly. This led to a flexible, software-based service known as the Domain Name System (DNS), which provided a flexible mechanism for identifying the hostname associated with an IP address, and vice versa. (For more information about DNS, see Chapter 32, "Setting Up a DNS Server.")

Why begin a chapter on DHCP (Dynamic Host Configuration Protocol) by discussing DHCP? Because DHCP and its predecessors were largely developed to address similar issues of scalability and flexibility by providing a similarly flexible service that could dynamically provide various types of network information. When hosts at a site are networked and those hosts are all located on the same subnet, assigning them static IP addresses and statically maintaining other IP-related information such as name-server identities is reasonable. However, as the number of hosts on a network grows and hosts are added more and more frequently, requiring that someone from IT manually install and configure each host's networking quickly becomes impracticals. Similarly, networked laptops are frequently used in multiple locations, each of which may require a different network configuration.

This chapter provides a bit of background information on DHCP and its predecessors, the types of problems that they were developed to, solve,

# IN THIS CHAPTER

+   - Overviewing DHCP

+   - Configuring a DHCP server from the command line

+   - Configuring a DHCP server graphically

+   - Troubleshooting DHCP