# Chapter 21 ♦ Configuring a DNS Server

# Table 21-1
Top-Level Domains

| TLD | Use |
|---|---|n| .com | Commercial organizations |
| .net | Network of machines |
| .org | Non-profit organizations |
| .mil | U.S. military |
| .gov | U.S. government |
| .co.uk | U.K. company |

# How Does a DNS Search Work?

We can take a look at how a DNS search takes place to put the idea of a distributed, hierarchical system into context.

+   1. Take our laptop as an example—the name lookup system is configured to get all name translations from our DNS server at 192.168.1.1. When we go to www.google.com, the laptop contacts 192.168.1.1 and asks it for the address of www.google.com. As our DNS server is a caching server (we talk about this later in the chapter), it contacts a DNS server to see if it knows.
2. The public DNS server at 194.106.56.6 accepts our request and attempts to find the IP address of Google for us. As this public DNS does not know the address directly (it does not control the Google domain), it asks a root DNS server if it knows the IP address of Google. Because the root servers do not control the Google domain, they tell our Internet service provider's domain server that it should ask the DNS server that controls the .com domain.
3. The public DNS queries the .com DNS server for the IP address of www.google.com. As the .com DNS server does not know the address directly, it refers the ISP to the DNS server that controls google.com domain (which the .com server knows).
4. The ISP asks the google server if it knows the address of www.google.com. This time we strike lucky, the DNS nameserver knows the address and returns this IP address to its ISP's DNS server.
5. When the ISP's DNS server knows the IP address, it passes this address back to our local DNS server, which finally returns it to our laptop.

As you can see, the DNS system works by servers cooperating with each other to find the answer to a DNS query. This helps to alleviate the burden of many resolution on a single root DNS server or a small group of root DNS servers.