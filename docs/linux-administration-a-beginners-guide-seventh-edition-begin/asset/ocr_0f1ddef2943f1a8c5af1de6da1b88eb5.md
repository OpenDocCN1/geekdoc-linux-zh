# CHAPTER 16 Domain Name System (DNS)

The TLDs can be broken down further:

+   - Generic top-level domain (such as .com, .net, .mil, .gov, .edu, .int, biz, and so on).

+   - Country-code top-level domains (such as .us, .uk, .ng, and .ca, corresponding to the country codes for the United States, the United Kingdom, Nigeria, and Canada, respectively), as well as their internationalized counterparts (such as Hindi for India, 中国 for China, р for Russia, and so on).

+   - The newly introduced top-level domains. These allow organizations to create any TLDs up to 64 characters. They can create generic words and brand names (such as .coke, .pepsi, .example, .linux, microsoft, caffenix, .who, .unicef, .company, .accountants, . and so on).

+   - Other special or infrastructure top-level domains (such as the .arpa domain).

The top-level domain in our sample FDN (serverA.example.org) is "org."

# The Second-Level Domain Names

The names in DNS make up the actual operational boundary of the namespaces. Internet service providers (ISPs), communities, nonprofit groups, and individuals typically acquire unique names within this. Here are examples: redhat.com, ubuntu.com, fedaproject.org, linuxservers.com, kernel.org, and caffenix.com.

The second-level domain in our sample FDN (serverA.example.org) is "example."

# The Third-Level Domain Names

Individuals and organizations that have been assigned second-level domain names can pretty much decide what to do with the third-level names. The convention, though, is to use the third-level names to reflect hostnames or other functions. It is also common for organizations to begin the subdomain definitions from here. An example of functional assignment of a third-level domain name is the "www" in the FDN www.yahoo.com. The "www" can be the actual hostname of a machine under the umbrella of the yahoo domain, or it can be an alias to a root hostname.

The third-level domain in our sample FDN (serverA.example.org) is "server." Here, it simply represents the actual hostname of our server.

By keeping DNS distributed in memory, the task of keeping track of all the hosts connected to the Internet is delegated to each site, which takes care of its information. The central repository of all primary name servers, called the root server, is the only list of existing domains. Obviously, a list of such a critical nature is itself mirrored across multiple servers and multiple geographic regions. For example, an earthquake in one part of the world might destroy the root server(s) for that area, but all the root servers in other unaffected parts of the world can take up the slack until the affected servers come back online. The only noticeable difference to users is likely to be a slightly higher latency in resolving domain names. Pretty amazing, isn't it? The inverted tree structure of DNS is shown in Figure 16-2.