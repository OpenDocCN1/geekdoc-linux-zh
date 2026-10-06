The dig utility displays a lot of information.

+   * The Authority Section specifies the primary name servers, and the Add-tional Section specifies the IP addresses that correspond to the names in the Authority Section.
* The SERVER line (toward the end) specifies the name and IP address of the DNS server that the local system uses: This is where dig gets its information.
* The second column specifies the TTL (page 1499) in seconds.
* IN in the third column is the query class and indicates that this is an Inter-net class query.
* SOA, MX, NS, or A in the fourth column specifies the type of information (DNS query type) that the row holds:
    * The NS (name server) record(s) specify name servers that upstate.edu uses. An NS record is meaningful only when you query a domain.
    * The MX (mail exchanger) record(s) specify a mail server for the domain you are querying. The upstate.edu domain has several mail-servers. The lower preference value (the number before the mail server domain in the right column), the higher the priority (ducserv6b is al-ways tried before ducserv3).
* There is one SOA (start or zone of authority) for a given domain. The SOA
    * Is the authoritative primary DNS for the domain.
    * Defines who the point of contact is for the domain.
    * Controls the TTL for records from the DNS.
    * Controls how often another name server will retry the domain's name server.
* Controls when another name server will timeout when trying to contact the domain's name server.
* The A (network Address) record specifies in the last column the IP ad-dress that corresponds to the domain name in the first column.

The dig utility has many query types. The any type is used in the preceding example. You can also use mx, ns, soa, and others. Refer to the dig man page for more details.

# whois: Looks Up Information about an Internet Site

The whos utility queries a who server for information about an Internet site. The utility returns site contact and InterNIC or other registry information that can help