Imagine you have a network and needed your own set of IPs. If you had only 5 computers, you’d still get 253 addresses. If you had no use for the other 248 addresses, they’d be wasted. With CIDR, you could be given a subnet that would just fit your needs and waste a minimum amount of addresses.

# VLSM

Under the Classful system, netmasks were set. Networks were divided on the octet boundaries only. Under Classless addressing, a new concept called *Variable Length Subnet Masks (VLSM)* was introduced. This is how CIDR is implemented.

> **Note**
> 
> CIDR and the RFCs allow for subnet masks that don’t translate to VLSM netmasks. However, these netmasks are really only good as a mental exercise and should never actually be implemented. These masks are fodder for advanced networking and will not be discussed in this text.

Before proceeding further, you’ll need four definitions. These are not the technical definitions of the terms, but are provided in layman’s terms:

+   - **Host Address**—A unique IP given to each separate communications device in a host. No two devices or systems on a network may have the same number. A host with two or more devices will have at least that number of unique IPs, but can have more (devices can have more than one IP each if required).
+   - **Network Address**—The lower boundary of a network that helps define the limits of the network. No host can be assigned the network address. This address will always be an even binary multiple.
+   - **Broadcast Address**—The upper boundary of a network that helps define the limits of the network. Although no host will ever be assigned the broadcast address, all hosts on the network that have IP stacks conformant to Internet standards will respond to queries to this address. This address will always be an even binary multiple minus 1.
+   - **Netmask**—The netmask defines the division between network and hosts. The netmask will be a binary number whereby all numbers to the left (network portion) are ones, and to the right (host portion) all zeroes.

> **Note**
> 
> All operating systems (some 104+) conform to the standard of the use of the broadcast address except Microsoft operating systems. This non-conformance on Microsoft’s part breaks some network utilities where Microsoft hosts are present on the network. This nuisance should be kept in mind when troubleshooting network problems.

When networks and subnets are discussed, the concept of a netmask comes up. Under the old Classful system, netmasks would be one of 255.255.255.0, 255.255.0.0, or 255.0.0.0. Note that this is equivalent to all ones in the first 24, 16, or 8 bits and zeroes in the last 8,