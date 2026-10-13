Table 34-8: Domain Name Service Resource Record Types

| Type | Description |
|------|-------------|
| SIG | Resource record signature |
| NXT | Next resource record |

# Start of Authority: SOA

A zone or reverse mapping file always begins with a special resource record called the Start of Authority (SOA) record. This record specifies that all the following records are authoritative for this domain. It also holds information about the name server's domain, which is to be given to other name servers. An SOA record has the same format as other resource records, though its data segment is arranged differently. The format for an SOA record follows:

```
name {ttl} class SOA Origin Person-in-charge (
    Serial number
    Refresh
    Retry
    Expire
    Minimum )
```

Each zone has its own SOA record. The SOA begins with the zone name specified in the named.conf zone entry. This is usually a domain name. An @ symbol is usually used for the name and acts like a macro expanding to the domain name. The class is usually the Internet class, IN. SOA is the type. Origin is the machine that is the origin of the records, usually the machine running your name server daemon. The person-in-charge is the e-mail address for the person managing the name server (use dots, not @, for the e-mail address, as this symbol is used for the domain name). Several configuration entries are placed in a block delimited with braces. The first is the serial number. You change the serial number when you add or change records, so that it is updated by other servers. The serial number can be any number, as long as it is incremented each time a change is made to any record in the zone. A common practice is to use the year-month-day-number for the serial number, where number is the number of changes in that day. For example, 1999120403 would be the year 1999, December 4, for the third change. Be sure to update it when making changes.

Refresh specifies the time interval for refreshing SOA information. Retry is the frequency for trying to contact an authoritative server. Expire is the length of time a secondary name server keeps information about a zone without updating it. Minimum is the length of time records in a zone live. The times are specified in the number of seconds.

The following example shows an SOA record. The machine running the name server is turtle.mytrek.com, and the e-mail address of the person responsible for the server is hostmaster.turtle.mytrek.com. Notice the periods at the ends of these names. For names with no periods, the domain name is appended. turtle would be the same as turtle.mytrek.com. When entering full hostnames, be sure to add the period so that the domain is not appended.

```
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
    1997022700 ; Serial
    28800 ; Refresh
    14400 ; Retry
    3600000 ; Expire
    86400 ) ; Minimum
```

# Name Server: NS