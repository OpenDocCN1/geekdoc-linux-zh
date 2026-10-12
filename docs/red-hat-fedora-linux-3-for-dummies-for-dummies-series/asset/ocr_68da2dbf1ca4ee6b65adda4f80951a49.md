+   Authoritative name servers: Every zone must have an authoritative name server. It holds the information for every host within the zone. You can create primary and secondary authoritative name servers. The secondary name servers back up the primary name servers.

+   Non-authoritative name servers: To present data that doesn't change much over time, you can create name servers that can load fast but don't have to provide the most up-to-date information.

+   Caching name server: Name servers can be configured to look up addresses from other name servers and temporarily save, or cache, the information. Caching name servers helps spread out the load of servicing large domains.

+   Root name servers: The authorities that control domain-name registrations provide root name servers that hold the addresses of name servers for each domain. DNS queries go to root name servers to find out where to find authoritative name servers.

The parameters found in DNS configuration and zone files are called resource records (RR). This list describes them:

+   A records: Address (A) records map IP names to numeric addresses.

+   C records: Canonical (C) records define aliases for A records.

+   MX records: Mail-exchange (MX) records specify the mail servers that service a domain.

+   NS records: Name-server (NS) records specify the name server for a zone.

+   SOA: The start-of-authority (SOA) parameter creates a section that describes the generic properties of a zone file. The SOA configures parameters that set the serial number and various timeouts, plus the domain name of a zone.

# # Getting a look at a DNS address request

This section gives you a quick look at the steps your browser takes to find the Fedora Core Web page:

+   1. You open your browser and enter any URL, such as `fedora.redhat.com`.

+   2. The browser asks Linux for the Web page's numeric IP address.

+   3. Linux looks in its `/etc/resolv.conf` configuration file and finds the address of a name server.