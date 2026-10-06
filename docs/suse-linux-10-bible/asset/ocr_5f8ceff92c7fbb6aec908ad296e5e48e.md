# # Configuring a DNS Server

We have talked about a few backbone services of the Internet in this book, but one of the most important ones is the role of the nameserver. Imagine life without names; going to your search engine (e.g., www.google.com) would involve you having to type http://66.102.11.104. Not so bad, but if you had ten favorite sites, you would have to remember all of those addresses. TCP/IP needs to use IP addresses to make a connection to another machine, the Domain Name System (DNS) is important to bridge the gap between the human and the computer. The role of DNS is not just to translate names to IP addresses, but also to form the basis for mail server lookups and reverse name lookups (IP addresses to names).

The most popular DNS server on the Internet is BIND (Berkeley Internet Name Daemon). BIND truly is an open source success, on par with Apache. Both are terribly important to the function of the Internet, and both are very well-written pieces of software.

# ## Some DNS Theory

As is customary in the Unix world, DNS is distributed and hierarchical in design. The DNS management is controlled locally in a domain, and this is something that may need to be explained. The dictionary tells us that domain is a “territory over which rule or control is exercised. The term *domain* has been used to describe a domain name, but its meaning is still the same, a territory over which control is exercised.

# ### In This Chapter

+   - DNS theory

+   - Configuring caching and forwarding

+   - Examining DNS record types

+   - Configuring zones