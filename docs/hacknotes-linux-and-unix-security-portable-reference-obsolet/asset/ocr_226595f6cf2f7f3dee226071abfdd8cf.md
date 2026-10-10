# Quering RIR Records by an IP Address or Network Block

To find out which organization is the owner of a particular block of IP addresses, try this form of the command:

```
whois -h whois.riwboisserver.net ipaddressorblock
```

The address 192.168.1.0/24 falls under an allocated block of IP addresses that are not routable. For more information on nonroutable IP ranges, please see RFC 1918, available at http://www.faqs.org/rfcs/rfc1918.html. Let us pretend that 192.168.1.0/24 is a valid and routable IP range for the purposes of our example. If we were to search whois.arin.net for this block, we would have to attempt such a query:

```
[bash]$ whois -h whois.arin.net 192.168.1.0
[whois.arin.net]
OrgName: Internet Assigned Numbers Authority
OrgID: IANA
NetRange: 192.168.0.0 - 192.168.255.255
CIDR: 192.168.0.0/16
NetName: IANA-CEMl
NetHandle: NET-192-168-0-0-1
Parent: NET-192-0-0-0-0
NetType: IANA Special Use
NameServer: BLACKHOLE-1.IANA.ORG
NameServer: BLACKHOLE-2.IANA.ORG
Comment: This block is reserved for special purposes.
Please see RFC 1918 for additional information.
RegDate: 1994-03-15
Updated: 2002-09-16
OrgTechHandle: IANA-ARIN
OrgTechName: Internet Corporation for Assigned Names and Number
OrgTechPhone: +1-234-567-8900
OrgTechEmail: res-ip@iana.org
# ARIN Whois database, last updated 2003-01-12 20:00
# Enter ? for additional hints on searching ARIN's Whois database.
```

# Quering RIR Records by Handle

Individual POCs and organizations listed on RIR whois servers have a handle associated with them. You can query a particular handle to find related contact information:

```
whois -h whois.riwboisserver.com "HANDLE"*
```

![](bbox=[0.87, 0.13, 0.97, 0.33])