create primary and secondary authoritative name servers. The secondaries back up the primaries.

+   Non-authoritative name servers: You can create name servers that don't necessarily provide the most up-to-date information.

+   Caching name server: Name servers can be configured to look up addresses from other name servers and temporarily save, or cache, the information. Caching name servers helps spread out the load of servicing large domains.

+   Root name servers: The authorities who control domain name registrations provide root name servers that hold the addresses of name servers for each domain. DNS queries go to root name servers to find out where to find authoritative name servers.

This list describes the parameters found in DNS configuration and zone files. The parameters are called resource records (RR):

+   A records: Address (A) records map IP names to numeric addresses.

+   C records: Canonical (C) records define aliases for A records.

+   MX records: Mail exchange (MX) records specify the mail servers that service a domain.

+   NS records: Name server (NS) records specify the name server for a zone.

+   SOA: The start of authority (SOA) parameter creates a section that describes the generic properties of a zone file. The SOA configures parameters that set the serial number and various timeouts, plus the domain name of a zone.

# ## Understanding how a DNS address request works

This section gives you a look at how your browser finds the Red Hat Linux Web page:

+   1.  You open your browser and enter the URL www.redhat.com.
2.  The browser asks Linux for the Web page’s numeric address.
3.  Linux looks in its /etc/resolv.conf configuration file and finds the address of a name server.