
![](img/a7eec43a54473e95dc5ea333fecf1bd7_706_0.png)

The rndc (remote name daemon control) utility is a successor to the older ndc (for name daemon controller) utility used to control the named server by sending it messages over a special control channel, a TCP port where named listens for messages. The rndc utility uses a cryptographic key to authenticate itself to the named server. The named server has the same cryptographic key so it can decode the authentication information sent by rndc.

After the options statement, the /etc/named.conf file contains several zone statements, each enclosed in curly braces and terminated by a semicolon. Each zone statement defines a zone. The first zone is named "." (root zone); it's a hint zone that specifies the root name servers.

The next two zone statements in /etc/named.conf are master zones. The syntax for a master zone statement for an Internet class zone (indicated by the IN keyword) is as follows:

```
zone "zone-name" IN {
    type master;
    file "zone-file";
    [...other optional statements...]
};
```

The zone-name is the name of the zone, and zone-file is the zone file that contains the resource records (RR) — the database entries — for that zone. I describe zone file formats and resource record formats in the next two sections.

## Zone file formats

The zone file typically starts with a number of directives, each of which begins with a dollar sign ($) followed by a keyword. Two commonly used directives are $TTL and $ORIGIN.

For example, the line

```
$TTL  86400
```

uses the $TTL directive to set the default Time To Live (TTL) for subsequent records with undefined TTLs. The value is in seconds, and the valid TTLs are in the range 0 to 2147483647 seconds. In this case, the directive sets the default TTL as 86400 seconds (or one day).

The $ORIGIN directive sets the domain name that will be appended to any unqualified records. For example, the following $ORIGIN directive sets the domain name to localhost:

```
$ORIGIN localhost.
```

If there is no $ORIGIN directive, the initial $ORIGIN is the same as the zone name that comes after the zone keyword in the /etc/named.conf file.

After the directives, the zone file contains one or more resource records. These records follow a specific format, which is outlined in the next section.

## Resource record (RR) formats

You have to understand the format of the resource records before you can understand and intelligently work with zone files. Each resource record has the following format (the optional fields are shown in square brackets):

```
[domain] [ttl] [class] type data [;comment]
```

The fields are separated by tabs or spaces and may contain some special characters, such as an @ symbol for the domain and a semicolon (;) to indicate the start of a comment.

The first field, which must begin at the first character of the line, identifies the domain. You can use the @ symbol to use the current $ORIGIN for the domain name for this record. If you have multiple records for the same domain name, leave the first field blank.

The optional ttl field specifies the Time To Live — the duration for which the data can be cached and considered valid. You can specify the duration in one of the following formats:

- N, where N is a number meaning N seconds
- NW, where N is a number meaning N weeks
- ND, where N is a number meaning N days
- NH, where N is a number meaning N hours
- NM, where N is a number meaning N minutes
- NS, where N is a number meaning N seconds

The letters W, D, H, M, and S can also be in lowercase. Thus, you can write 86400 or 1D (or 1d) to indicate a duration of one day. You can also combine these to specify more precise durations, such as 5w6d16h to indicate 5 weeks, 6 days, and 16 hours.

The class field specifies the network type. The most commonly used value for this field is IN for Internet.

Next in the resource record is the type field, which denotes the type of record (such as SOA, NS, A, or PTR). Table 5-1 lists the DNS resource record types. The data field comes next, and it depends on the type field.

### Table 5-1 DNS Resource Record Types

| Type | Name | Description |
|------|------|-------------|
| SOA | Start of Authority | Indicates that all subsequent records are authoritative for this zone. |
| NS | Name Server | Identifies authoritative name servers for a zone. |
| A | Address | Specifies the IP address corresponding to a host name. |
| PTR | Pointer | Specifies the name corresponding to an address (used for reverse mapping — converting an IP address to a host name). |
| MX | Mail Exchanger | Identifies the host that accepts mail meant for a domain (used to route e-mail). |
| CNAME | Canonical Name | Defines the nickname or alias for a host name. |
| KEY | Public Key | Stores a public key associated with a DNS name. |
| CERT | Digital Certificate | Holds a digital certificate. |
| HINFO | Host Info | Identifies the hardware and operating system for a host. |
| RP | Responsible Person | Provides the name of a technical contact for a domain. |
| SRV | Services | Lists well-known network services provided by the domain. |
| TXT | Text | Used to include comments and other information in the DNS database. |

You should learn to read the resource records, at least the ones of type SOA, NS, A, PTR, and MX, which are some of the most commonly used. Next, I briefly describe these records, illustrating each record type through an example.

A typical SOA record has the following format:

```
@  1D  IN  SOA
@  root (
    42          : serial
    3H          : refresh -- 3 hours
    15M         : retry -- 15 minutes
    1W          : expiry -- 1 week
    1D )        : minimum -- 1 day
```

The first field specifies the domain as an @, which means the current domain (by default, the zone name, as shown in the /etc/named.conf file). The next field specifies a TTL of one day for this record. The class field is set to IN, which means the record is for Internet. The type field specifies the record type as SOA. The rest of the fields constitute the data for the SOA record. The data includes the name of the primary name server (in this case, @ or the current domain), the e-mail address of the technical contact, and five different times enclosed in parentheses.

The NS record specifies the authoritative name servers for a zone. A typical NS record looks like the following:

```
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

In this case, the NS record lists the authoritative name server for the root zone (notice that the name of the first field is a single dot). The Time-To-Live field specifies the record to be valid for 1,000 hours (3,600,000 seconds). The class is IN, for Internet; and the record type is NS. The final field lists the name of the name server (A.ROOT-SERVERS.NET.), which ends with a dot.

An A record specifies the address corresponding to a name. For example, the following A record shows the address of A.ROOT-SERVERS.NET. as 198.41.0.4:

```
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

In this case, the network class isn't specified because the field is optional, and the default is IN. PTR records are used for reverse mapping — converting an address to a name. Consider the following example:

```
1 IN PTR localhost.
```

This record comes from a file for a zone named 0.0.127.in-addr.arpa. Therefore, this record says that the name associated with the address 127.0.0.1 is localhost. An MX record specifies the name of a host that accepts mail on behalf of a specific domain. For example, here's a typical MX record: naba IN MX 10 mailhub.lnbsoft.com. This says that mail addressed to the host named naba in the current domain should be sent to mailhub.lnbsoft.com (this host is called a mail exchanger). The number 10 is the preference value. For a list of multiple MX records with different preference values, the ones with lower preference values are tried first. Armed with this bit of information about resource records, you can go through the zone files for the caching name server.
