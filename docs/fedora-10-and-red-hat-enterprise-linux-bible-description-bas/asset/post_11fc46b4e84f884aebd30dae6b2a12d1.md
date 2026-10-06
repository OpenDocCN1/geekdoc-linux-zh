
# Chapter 25: Making Servers Public with DNS 977

## Setting up the zone files (inside)

/var/named/chroot/var/named directory contains the zone files that the /var/named/chroot/etc/named.conf file points to. For the example, you need to create only three zone files from scratch. You can (and should) leave the named.ca file alone.

Most of the real work of the domain name server occurs in the zone files. In the example, the db.yourdomain.com.inside contains the basic records for the yourdomain.com, including all private names and addresses. The following is an example of that:

```
TTL      86400               hostmaster.yourdomain.com.
@        IN  SOA  yourdomain.com.
                        2008042701 ; Serial
                        28800               ; Refresh
                        14400               ; Retry
                        360000              ; Expire
                        86400 )             ; Minimum

; Name servers
         IN  NS  ns1.yourdomain.com.
         IN  NS  ns2.yourdomain.com.

; Mail server for domain
         IN  MX 10  mail.yourdomain.com.

; Public servers
ns1       IN  A  10.0.0.1
ns2       IN  A  10.0.0.2
mail      IN  A  123.45.67.2
www       IN  A  123.45.67.3
ftp       IN  A  123.45.67.4

; Private clients on the LAN
red       IN  A  10.0.0.2
blue      IN  A  10.0.0.3
green     IN  A  10.0.0.4
yellow    IN  A  10.0.0.5
```

; EOF

The zone file for your “inside” yourdomain.com contains resource records that include information about the zone. Your DNS server uses the TTL (time-to-live) to tell name servers that store the information you provide for this domain how they can keep the information before they need to throw it out and get fresh information. The first value is the default for the entire zone, and the time is in seconds. So a value of 86,400 indicates that a client is using the information should obtain fresh records about this domain every 24 hours.

# Part IV: Fedora RHEL Network and Server Setup

The SOA line identifies the authority for the domain. The at (@) sign represents yourdomain.com name — the dot (.) must appear at the end of the domain name. The dot represents the root of the Internet. If you leave the dot out, your DNS server appends the domain name, so the DNS server will use the name yourdomain.comyourdomain.com. The hostmaster@yourdomain.com string indicates the e-mail address of the person who is to receive e-mail regarding the domain. (The dot changes to an @ sign, resulting in hostmaster@yourdomain.com). Other information regarding the SOA record is as follows:

- Start with any number. If the zones record change, the serial number to alert other servers that they get fresh data about your domain.

CAUTION: If you forget to increase the serial number after changing zone records, other servers that cache this data never pick up your changes. To help remember, use the date in the serial number. The number 2008042701 was for April 27, 2008. The 01 represents the first change made on that day.

- Refresh — Defines how the slave DNS server for the zone checks for changes.

The name server (NS) records define the name servers that represent this zone. In case NS records define hosts with the names ns1 and ns2 in yourdomain.com. The MX record indicates the location of the master server for the domain, so that the DNS server can direct e-mail to users in yourdomain.com. The rest of the file defines IP addresses for the private clients and public servers that are associated with the domain. Note that the server at address 10.0.0.2 serves as a client on the LAN and a DNS server.

## Setting up the zone files (outside)

For the "outside" you made a db.yourdomain.comoutside using the file from the "inside" file, with the following exceptions:

- Removed all references to private clients on the LAN. That way, someone poking around the Internet can't get information about your computers.
- Changed the addresses of the primary and slave DNS servers (ns1 and ns2) to 123.45.67.1 and 123.45.67.2, respectively. In that way, only public addresses for name servers are seen by the public. (Of course, you need to use your own IP addresses instead of the 123.45.67.1 and 123.45.67.2).

## Setting up the zone files (reverse lookup)

The other new file in the example is the yourlan.db file, which contains the information necessary to perform reverse IP lookups for the computers on your LAN. Here's an example:

```
TTL    86400
IN      SOA nsl.yourdomain.com hostmaster.yourdomain.com. (
                2006042701 : Serial
                28800 : Refresh
                0 : Retry
                360000 : Expire
                86400 ) : Minimum
IN      NS    nsl.yourdomain.com.
IN      PTR yourdomain.com.
IN      PTR red.
IN      PTR blue.
IN      PTR green.
IN      PTR yellow.
```

The zone file for your “inside” yourdomain.com contains resource records that include information about the zone. Your DNS server uses the TTL (time-to-live) to tell name servers that store the information you provide for this domain how they can keep the information before they need to throw it out and get fresh information. The first value is the default for the entire zone, and the time is in seconds. So a value of 86,400 indicates that a client is using the information should obtain fresh records about this domain every 24 hours.

The SOA line identifies the authority for the domain. The at (@) sign represents yourdomain.com name — the dot (.) must appear at the end of the domain name. The dot represents the root of the Internet. If you leave the dot out, your DNS server appends the domain name, so the DNS server will use the name yourdomain.comyourdomain.com. The hostmaster@yourdomain.com string indicates the e-mail address of the person who is to receive e-mail regarding the domain. (The dot changes to an @ sign, resulting in hostmaster@yourdomain.com). Other information regarding the SOA record is as follows:

- Start with any number. If the zones record change, the serial number to alert other servers that they get fresh data about your domain.

CAUTION: If you forget to increase the serial number after changing zone records, other servers that cache this data never pick up your changes. To help remember, use the date in the serial number. The number 2008042701 was for April 27, 2008. The 01 represents the first change made on that day.

- Refresh — Defines how the slave DNS server for the zone checks for changes.

The name server (NS) records define the name servers that represent this zone. In case NS records define hosts with the names ns1 and ns2 in yourdomain.com. The MX record indicates the location of the master server for the domain, so that the DNS server can direct e-mail to users in yourdomain.com. The rest of the file defines IP addresses for the private clients and public servers that are associated with the domain. Note that the server at address 10.0.0.2 serves as a client on the LAN and a DNS server.

The other new file in the example is the yourlan.db file, which contains the information necessary to perform reverse IP lookups for the computers on your LAN. Here's an example:

```
TTL    86400
IN      SOA nsl.yourdomain.com hostmaster.yourdomain.com. (
                2006042701 : Serial
                28800 : Refresh
                0 : Retry
                360000 : Expire
                86400 ) : Minimum
IN      NS    nsl.yourdomain.com.
IN      PTR yourdomain.com.
IN      PTR red.
IN      PTR blue.
IN      PTR green.
IN      PTR yellow.
```

(Wait, the OCR text had some repetitions and garble in the middle. I will provide the clean logical flow based on the provided segments.)

[Self-correction: The OCR text provided contains significant overlapping and garbled sections. I will de-duplicate and clean the flow based on the instructions provided.]

[content]
# Chapter 25: Making Servers Public with DNS 977

## Setting up the zone files (inside)

/var/named/chroot/var/named directory contains the zone files that the /var/named/chroot/etc/named.conf file points to. For the example, you need to create only three zone files from scratch. You can (and should) leave the named.ca file alone.

Most of the real work of the domain name server occurs in the zone files. In the example, the db.yourdomain.com.inside contains the basic records for the yourdomain.com, including all private names and addresses. The following is an example of that:

```
TTL      86400               hostmaster.yourdomain.com.
@        IN  SOA  yourdomain.com.
                        2008042701 ; Serial
                        28800               ; Refresh
                        14400               ; Retry
                        360000              ; Expire
                        86400 )             ; Minimum

; Name servers
         IN  NS  ns1.yourdomain.com.
         IN  NS  ns2.yourdomain.com.

; Mail server for domain
         IN  MX 10  mail.yourdomain.com.

; Public servers
ns1       IN  A  10.0.0.1
ns2       IN  A  10.0.0.2
mail      IN  A  123.45.67.2
www       IN  A  123.45.67.3
ftp       IN  A  123.45.67.4

; Private clients on the LAN
red       IN  A  10.0.0.2
blue      IN  A  10.0.0.3
green     IN  A  10.0.0.4
yellow    IN  A  10.0.0.5
```

; EOF

The zone file for your "inside" yourdomain.com contains resource records that include information about the zone. Your DNS server uses the TTL (time-to-live) to tell name servers that store the information you provide for this domain how they can keep the information before they need to throw it out and get fresh information. The first value is the default for the entire zone, and the time is in seconds. So a value of 86,400 indicates that a client is using the information should obtain fresh records about this domain every 24 hours.

# Part IV: Fedora RHEL Network and Server Setup

The SOA line identifies the authority for the domain. The at (@) sign represents yourdomain.com name — the dot (.) must appear at the end of the domain name. The dot represents the root of the Internet. If you leave the dot out, your DNS server appends the domain name, so the DNS server will use the name yourdomain.comyourdomain.com. The hostmaster@yourdomain.com string indicates the e-mail address of the person who is to receive e-mail regarding the domain. (The dot changes to an @ sign, resulting in hostmaster@yourdomain.com). Other information regarding the SOA record is as follows:

- Start with any number. If the zones record change, the serial number to alert other servers that they get fresh data about your domain.

CAUTION: If you forget to increase the serial number after changing zone records, other servers that cache this data never pick up your changes. To help remember, use the date in the serial number. The number 2008042701 was for April 27, 2008. The 01 represents the first change made on that day.

- Refresh — Defines how the slave DNS server for the zone checks for changes.

The name server (NS) records define the name servers that represent this zone. In case NS records define hosts with the names ns1 and ns2 in yourdomain.com. The MX record indicates the location of the master server for the domain, so that the DNS server can direct e-mail to users in yourdomain.com. The rest of the file defines IP addresses for the private clients and public servers that are associated with the domain. Note that the server at address 10.0.0.2 serves as a client on the LAN and a DNS server.

## Setting up the zone files (outside)

For the "outside" you made a db.yourdomain.comoutside using the file from the "inside" file, with the following exceptions:

- Removed all references to private clients on the LAN. That way, someone poking around the Internet can't get information about your computers.
- Changed the addresses of the primary and slave DNS servers (ns1 and ns2) to 123.45.67.1 and 123.45.67.2, respectively. In that way, only public addresses for name servers are seen by the public. (Of course, you need to use your own IP addresses instead of the 123.45.67.1 and 123.45.67.2).

## Setting up the zone files (reverse lookup)

The other new file in the example is the yourlan.db file, which contains the information necessary to perform reverse IP lookups for the computers on your LAN. Here's an example:

```
TTL    86400
IN      SOA nsl.yourdomain.com hostmaster.yourdomain.com. (
                2006042701 : Serial
                28800 : Refresh
                0 : Retry
                360000 : Expire
                86400 ) : Minimum
IN      NS    nsl.yourdomain.com.
IN      PTR yourdomain.com.
IN      PTR red.
IN      PTR blue.
IN      PTR green.
IN      PTR yellow.
```

## Starting the named (DNS) daemon

To start the named daemon and see whether it's working, type the following (as root):

```
# /etc/init.d/named start
```

If the named daemon starts successfully, clients of your server should start getting information about your domain. To set the named daemon to start each time the system boots up, type the following:

```
# chconfig named
```

Remember that when you make changes to named.conf or any of the zone files, you must increase the serial number before checking your domain. After, you should restart the named service (as root) as follows:

```
# /etc/init.d/named restart
```

Then you should consider adding your server's local address to its //resolv.conf file. For example, the /etc/resolv.conf file could include the following:

```
search yourdomain.com
nameserver 127.0.0.1
```

## Checking that DNS is working

The best way to verify your DNS server is working correctly is to watch it in action. Here are a few commands you can use to check out your DNS server. The first example uses the host command to get the IP address for the host computer blue in the local domain:

```
# host blue
blue.yourdomain.com has address 10.0.0.3
```
