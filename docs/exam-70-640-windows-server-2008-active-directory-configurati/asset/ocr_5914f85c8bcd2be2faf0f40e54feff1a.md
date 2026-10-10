# ### Understanding Reverse Name Resolution

> Sometimes a computer needs to convert an IP address into a DNS name. This conversion process is known as *reverse name resolution*.

Because the domain hierarchy is separated into domain names, there is no practical way to resolve an IP address into a name using iterative queries. You could forward the reverse name resolution request to every DNS server on the Internet in search of the requested address, but that would be impractical.

The DNS developers created a special domain called *in-addr.arpa* that is specifically designed for reverse name resolution. The in-addr.arpa second-level domain contains four additional levels of subdomains, with each level consisting of subdomains that are named using the numerals 0 to 255. For example, beneath in-addr.arpa are 256 third-level domains, which have names ranging from 0.in-addr.arpa to 255.in-addr.arpa. Each of the 256 third-level domains can have 256 fourth-level domains below it, numbered from 0 to 255. This is also true of each fourth-level domain, which can have 256 fifth-level domains, numbered from 0 to 255, and each fifth-level domain, which can have up to 256 hosts in it, numbered from 0 to 255.

Using this hierarchy of subdomains, it is possible to express the first three bytes of an IP address as a DNS domain name and to create a resource record named for the fourth byte in the appropriate fifth-level domain. For example, to resolve the IPv4 address 192.168.89.34 into a name, a DNS server locates a domain named 89.168.192.in-addr.arpa and reads the contents of a special type of resource record called 34 in that domain. Address-to-name mappings use a special type of resource record called a Pointer (PTR), which was discussed earlier. For an IPv6 address of 4321::1:2:3:4:567:89ab, the reverse lookup record is ba.9.8.7.6.5.0.4.0.0.0.3.0.0.0.2.0.0.0.1.0.0.0.0.0.1.2.3.4.ip6.arpa.

# ### Combining Internal and External DNS Name Resolution

> The majority of modern organizations maintain an internal network as well as a public Internet presence. To provide name resolution for both internal and external clients, these two namespaces must be carefully managed so that clients can access resources in a seamless and secure fashion.

From a design perspective, there are a number of different options for combining an organization's public and private DNS presence. When you design a DNS namespace that includes both internal and external domains, you can use the following strategies:

+   *   **Use the same domain name internally and externally.** Microsoft strongly discourages the practice of using the same domain name for your internal and external namespaces. When you create an internal domain and an external domain with the same name, you make it possible for a computer in the internal network to have the same DNS name as a computer on the external network. This duplication wreaks havoc with the name resolution process. (You could make this arrangement work by copying all the zone data from your external DNS servers to your internal DNS servers, but the extra administrative difficulties make this a less than ideal solution.)

+   *   **Create separate and unrelated internal and external domains.** When you use different domain names for your internal and external networks, you eliminate the potential name resolution conflicts that result from using the same domain name for both networks. However, this solution requires you to register two domain names and to maintain two separate DNS namespaces. The different domain names can also be a potential source of confusion to users who have to distinguish between internal and external resources.

+   *   **Make the internal domain a subdomain of the external domain.** This solution involves internal and external networks to register a single Internet domain name and