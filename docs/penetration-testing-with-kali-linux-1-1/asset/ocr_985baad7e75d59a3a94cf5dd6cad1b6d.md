# 7. Active Information Gathering

In this module, we will move beyond passive information gathering and explore techniques that involve direct interaction with target services. We will take a look at some foundational techniques but bear in mind there are innumerable services that can be targeted in the field. This includes Active Directory for example, which we cover in more detail in a separate module. However, we will look at some of the more common active information gathering techniques in this module including port scanning and DNS, SMB, NFS, SMTP, and SNMP enumeration.

# 7.1 DNS Enumeration

The Domain Name System (DNS) ${ }^{187}$ is one of the most critical systems on the Internet and is a distributed database responsible for translating user-friendly domain names into IP addresses.

This is facilitated by a hierarchical structure that is divided into several zones, starting with the top-level root zone. Let’s take a closer look at the process and servers involved in resolving a hostname like www.megacorpoone.com.

The process starts when a hostname is entered into a browser or other application. The browser passes the hostname to the operating system’s DNS client and the operating system then forwards the request to the external DNS server it is configured to use. This first server in the chain is known as the DNS Recursor and is responsible for interacting with the DNS infrastructure and returning the results to the DNS client. The DNS recursor contacts one of the servers in the DNS root zone. The root server then responds with the address of the server responsible for the zone containing the Top Level Domain (TLD), ${ }^{188}$ in this case, the .com TLD.

Once the DNS recursor receives the address of the TLD DNS server, it queries it for the address of the authoritative name server for the megacorpoone.com domain. The authoritative name server is the final step in the DNS lookup process and contains the DNS records in a local database known as the zone file. It typically hosts two zones for each domain, the forward lookup zone that is used to find the IP address of a specific hostname and the reverse lookup zone (if configured by the administrator), which is used to find the hostname of a specific IP address. Once the DNS recursor provides the DNS client with the IP address for www.megacorpoone.com, the browser can contact the correct web server at its IP address and load the webpage.

To improve the performance and reliability of DNS, DNS caching is used to store local copies of DNS records at various stages of the lookup process. It is for this reason that some modern applications, such as web browsers, keep a separate DNS cache. In addition, the local DNS client of the operating system also maintains its own DNS cache along with each of the DNS servers in the lookup process. Domain owners can also control how long a server or client caches a DNS record via the Time To Live (TTL) field of a DNS record.

${ }^{187}$ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Domain_Name_System

${ }^{188}$ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Top-level_domain