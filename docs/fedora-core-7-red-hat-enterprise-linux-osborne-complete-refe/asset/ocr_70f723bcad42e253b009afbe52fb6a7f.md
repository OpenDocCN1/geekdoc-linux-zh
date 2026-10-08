![](bbox=[0.68, 0.08, 0.89, 0.21])

# # Domain Name System

The Domain Name System (DNS) is an Internet service that locates and translates domain names into their corresponding Internet Protocol (IP) addresses. As you may recall, all computers connected to the Internet are addressed using an IP address. As a normal user on a network might have to access many different hosts, keeping track of the IP addresses needed quickly became a problem. It was much easier to label hosts with names and use the names to access them. Names were associated with IP addresses. When a user used a name to access a host, the corresponding IP address was looked up first and then used to provide access.

With the changeover from IPv4 to IPv6 address, DNS servers will have some configuration differences. Both are covered here, though some topics will use IPv4 addressing for better clarity, as they are easier to represent. IPv4 and IPv6 addressing are discussed in detail in Chapter 35.

# ## DNS Address Translations

The process of translating IP addresses into associated names is fairly straightforward. Small networks can be set up easily, with just the basic configuration. The task becomes much more complex when you deal with larger networks and with the Internet. The sheer size of the task can make DNS configuration a complex operation.

# ## Fully Qualified Domain Names

IP addresses were associated with corresponding names, called fully qualified domain names. A *fully qualified domain name* is composed of three or more segments. The first segment is the name that identifies the host, and the remaining segments are for the network in which the host is located. The network segments of a fully qualified domain name are usually referred to simply as the domain name, while the host part is referred to as the hostname (though this is also used to refer to the complete fully qualified domain name). In effect, subnets are referred to as domains. The fully qualified domain name **www.linux.org** could have an IPv4 address 198.182.196.56, where 198.182.196 is the network address and 56 is the host ID. Computers can be accessed only with an IP address, so a fully qualified domain name must first be translated into its corresponding IP address to be of any use. The parts of the IP address that make up the domain name and the hosts can vary. See Chapter 35 for a detailed discussion of IP addresses, including network classes and Classless Interdomain Routing (CIDR).