# The Role of DNS

The Domain Name System (DNS) tells the SMTP server when mail needs to be routed to another server instead of the end system.

# The Role of DNS

All Internet connections depend on IP addresses. DNS is a distributed database system that maps hostnames to IP addresses. However, DNS can do much more than just map addresses. Address (A) database records are only part of the story. DNS running on Linux supports about 40 different database record types.

> Some knowledge about DNS is needed to fully understand e-mail architecture. However, this is not a book about DNS. If you need to run a DNS server, see DNS Server Administration by Craig Hunt (Syex, 2000), part of the Craig Hunt Linux Library.

DNS database records have the same basic format. For the purposes of this, the format of DNS database records can be simplified to three basic fields:

+   * The name field contains the name of the object to which the record applies. Generally, this is a domain name or hostname.
* The type field contains the database record type. For example, an address record has a type field that contains the letter A.
* The data field contains the specific type of record. For example, an address record contains an IP address in the data field.

The forty possible record types, only a handful are used to build real DNS databases. Of this handful of records, one of the most important is the Mail Exchange (MX) record. MX records tell Sendmail where to deliver mail. The name field contains the hostname that appears in the e-mail address, and the data field contains the hostname of the server to which the mail should be delivered. Two MX records that define the mail servers for the foobirds.org domain contain the following:

```
foobirds.org. MX      10 wren.foobirds.org.
foobirds.org. MX      20 parrot.foobirds.org.
```

The name field contains the domain name foobirds.org., meaning that these records pertain to the entire domain. If mail is addressed to user@foobirds.org, the mail is directed to the mail changers defined by these records. This is a popular configuration, particularly when combined with the ability of the mail server to masquerade the name in outbound mail. Masquerading makes it look as if the mail sent by the local user