After you feel that your server is secure and correctly configured, your last step is to start up the server on the Internet with a domain name that points to it. You can either ask your service provider to configure DNS for you, or you can set up your own DNS server, as I describe in the following section.

# # Setting up a Domain Name System (DNS) Server

The *Domain Name System* (DNS) is essentially a distributed database that translates host names into IP addresses (and IP addresses back to host names). That database also contains information that relates to each domain, such as how the domain is organized into zones, where to route mail for that domain, and who to contact with questions associated with the domain.

In setting up your DNS server, you become part of a hierarchy of DNS servers that make up the Internet. At the top of this hierarchy is the root server, represented by a dot ( `.` ). Below the root server are the Top Level Domains, or TLDs (such as `.com` , `.org` , `.net` , and so on). Domains that individual organizations own and maintain lie below the TLDs. That’s where you come in.

As someone who’s setting up a DNS server, you’re responsible for managing the host names and IP addresses for the computers in the domain (or domains) for which you’re responsible. Keeping your DNS information correct means that people can access the services that you want to share, and the Internet as a whole works that much better as a result.

Besides using your DNS server to help people from the Internet find the public servers in your domain, you can also use DNS to provide name and IP address mapping for computers on your private network. The example in the “DNS name server example” section later in this chapter describes how to configure both private and public name and IP address records for a domain.

# ## Understanding DNS

The basic function of a *name server* is to answer queries by providing the information that those queries request. A DNS name server is primarily interested in translating domain and host names into IP addresses. A couple different kinds of servers provide this service, as the following list describes:

+   - **Primary (master) name server:** This name server contains authoritative information about the domains that it serves. In response to queries for information about its domains, this server provide that information marked as being authoritative. The primary is the ultimate source for data about the domain. The secondary name server only carries the same authority in that it has received and loaded a complete set of domain information from the primary.

+   - **Secondary (slave) name server:** This name server gets all information for the domain from the primary name server. As is the case for the primary, DNS considers the secondary’s information about the domain that it serves authoritative. (You set