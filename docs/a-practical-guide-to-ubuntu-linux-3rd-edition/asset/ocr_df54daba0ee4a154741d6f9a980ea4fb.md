![](bbox=[0.22, 0.09, 0.93, 0.4])

**Figure 24-1** The DNS domain structure (FQDNs are shown below hostnames.)

describes the path to the file being identified (for example, /var/spool/cups). Unlike a Linux pathname, you read a DNS domain name from right to left: It starts with the root domain at the right (represented by a period [.] ) and, as you read to the left, works its way down through the top-level and second-level domains to a subdomain or host. Frequently the name of the root domain (the period at the right) is omitted from a domain name.

**Domain** The term *domain* refers both to a single node in the DNS domain structure and to a catenated, period-separated list (path) of domain names that describes the location of a domain.

**FQDN** A fully qualified domain name (FQDN) is the DNS equivalent of a filesystem’s absolute pathname: It is a pointer that positively locates a domain on the Internet. Just as you (and Linux) can identify an absolute pathname by its leading slash ( / ) that represents the root directory, so an FQDN can be identified by its trailing period ( . ) that names the root domain (Figure 24-2).

![](bbox=[0.27, 0.77, 0.76, 0.9])

**Figure 24-2** A fully qualified domain name (FQDN)