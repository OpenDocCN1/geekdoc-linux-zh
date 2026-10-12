
```
F.ROOT-SERVERS.NET.
.   6D IN NS  B.ROOT-SERVERS.NET.
.   6D IN NS  J.ROOT-SERVERS.NET.
.   6D IN NS  K.ROOT-SERVERS.NET.
.   6D IN NS  L.ROOT-SERVERS.NET.
.   6D IN NS  M.ROOT-SERVERS.NET.
.   6D IN NS  I.ROOT-SERVERS.NET.
.   6D IN NS  E.ROOT-SERVERS.NET.
.   6D IN NS  D.ROOT-SERVERS.NET.
.   6D IN NS  A.ROOT-SERVERS.NET.

 ;; ADDITIONAL SECTION:
H.ROOT-SERVERS.NET.    5w6d16h IN A  128.63.2.53
C.ROOT-SERVERS.NET.    5w6d16h IN A  192.33.4.12
G.ROOT-SERVERS.NET.    5w6d16h IN A  192.112.36.4
F.ROOT-SERVERS.NET.    5w6d16h IN A  192.5.5.241
B.ROOT-SERVERS.NET.    5w6d16h IN A  128.9.0.107
J.ROOT-SERVERS.NET.    5w6d16h IN A  198.41.0.10
K.ROOT-SERVERS.NET.    5w6d16h IN A  193.0.14.129
L.ROOT-SERVERS.NET.    5w6d16h IN A  198.32.64.12
M.ROOT-SERVERS.NET.    5w6d16h IN A  202.12.27.33
I.ROOT-SERVERS.NET.    5w6d16h IN A  192.36.148.17
E.ROOT-SERVERS.NET.    5w6d16h IN A  192.203.230.10
D.ROOT-SERVERS.NET.    5w6d16h IN A  128.8.10.90
A.ROOT-SERVERS.NET.    5w6d16h IN A  198.41.0.4

 ;; Total query time: 4489 msec
 ;; FROM: lustre to SERVER: j.root-servers.net 198.41.0.10
 ;; WHEN: Mon Sep 10 04:18:26 2001
 ;; MSG SIZE  sent: 17  rcvd: 436
```

## The Zone File

The zone `0.0.127.in-addr.arpa` section in `named.conf` says that we are a master name-server for that zone and that the zone data is in the file `127.0.0`. Before examining the first real zone file in detail, look at the general format of a resource record specification:

name   TTL   class   type   data

Here, name is the DNS name with which this record is associated. In a zone file, names ending with a "." are fully qualified, whereas others are relative to the name of the zone. In the zone `example.com`, `foo` refers to the fully qualified name `foo.example.com`. The special name @ is a short form for the name of the zone itself. If the name is omitted, the last specified name is used again.

The `TTL` (*Time To Live*) field is a number that specifies the time for which the record can be cached. This is explained in greater detail in the discussion of the `SOA` record in the next section. If this field is omitted, the default `TTL` for the zone is assumed. `TTL` values are usually in seconds, but you can append an `m` for minutes, `h` for hours, or `d` for days.

BIND supports different record classes, but for all practical purposes, the only important class is `IN`, for Internet. If no class is explicitly specified, a default value of `IN` is assumed; to save a little typing, we do not mention the class in any of the zone files we write here.

The *type* field is mandatory and names the `RR` in use, such as `A`, `NS`, `MX`, or `SOA`. (We use only a few of the existing `RR`s here. Consult the DNS standards for a complete list.)

The *data* field (or *fields*) contains data specific to this type of record. The appropriate syntax will be introduced as we examine the use of each `RR` in turn.

Here is the zone file for the `0.0.127.in-addr.arpa` zone:

```
$TTL 2D
@	SOA	localhost. hostmaster.example.com. (
		2001090101	; Serial
		24h		; Refresh
		2h		; Retry
		3600000	; Expire (1000h)
		1h)		; Minimum TTL

	NS	localhost.
1	PTR	localhost.
```

The `$TTL` directive that should begin every *zone* file sets the default minimum time to live for the zone to two days. This is discussed further in the next section.

### The Zone File's SOA Record

The second line in the *zone* file uses the special `@` name that you saw earlier. Here, it stands for `0.0.127.in-addr.arpa`, to which the `SOA` (*Start of Authority*) record belongs. The rest of the fields (continued until the closing parenthesis) contain `SOA`-specific data.

The first data field in the `SOA` record is the fully qualified name of the master nameserver for the domain. The second field is the email address of the contact person for the zone. It is written as a DNS name by replacing the `@` sign with a `"."`; `foo@example.com` would be written as `foo.example.com.` (note the trailing `.`).

Do not use an address such as `a.b@example.com` because it is written as `a.b.example.com` and will later be misinterpreted as `a@b.example.com`.

> **TIP:**
> It is important to ensure that mail to the contact email address specified in the **SOA** field is frequently read because it is used to report DNS setup problems and other potentially useful information.

The next several numeric fields specify various characteristics of this zone. These values must be correctly configured, and for you to do so, you must understand each field. As shown in the comments (note that zone file comments are not in the same syntax as `named.conf` comments), the fields are serial number, refresh interval, retry time, expire period, and minimum TTL.

Serial numbers are 32-bit quantities that can hold values between 0 and 4,294,967,295 ($2^{32}-1$). Every time the zone data is changed, the serial number must be incremented. This change serves as a signal to slaves that they need to transfer the contents of the zone again. It is conventional to assign serial numbers in the format `YYYYMMDDNN`; that is, the date of the change and a two-digit revision number (for example, **2001090101**). For changes made on the same day, you increment only the revision. This reasonably assumes that you make no more than 99 changes to a zone in one day. For changes on the next day, the date is changed and the revision number starts from 01 again.

The refresh interval specifies how often a slave server should check whether the master data has been updated. It has been set to 24 hours here, but if the zone changes often, the value should be lower. Slaves can reload the zone much sooner if both they and the master support the **DNS NOTIFY** mechanism, and most DNS software does.

The retry time is relevant only when a slave fails to contact the master after the refresh time has elapsed. It specifies how long it should wait before trying again. (It is set to two hours here.) If the slave is consistently unable to contact the master for the length of the expire period (usually because of some catastrophic failure), it discards the zone data it already has and stops answering queries for the zone. Thus, the expire period should be long enough to allow for the recovery of the master nameserver. It has been repeatedly shown that a value of one or two weeks is too short. One thousand hours (about six weeks) is accepted as a good default.

As you read earlier, every RR has a TTL field that specifies how long it can be cached before the origin of the data must be consulted again. If the RR definition does not explicitly specify a TTL value, the default TTL (set by the $TTL directive) is used instead. This enables individual RRs to override the default TTL value as required.

The **SOA TTL**, the last numeric field in the SOA record, is used to determine how long negative responses (**NXDOMAIN**) should be cached. (That is, if a query results in an **NXDOMAIN** response, that fact is cached for as long as indicated by the **SOA TTL**.) Older versions of BIND used the **SOA minimum TTL** to set the default TTL, but BIND 9 no longer does so. The default TTL of 2 (two days) and SOA TTL of 1 (one hour) are recommended for cache friendliness.

The values used previously are good defaults for zones that do not change often. You might have to adjust them a bit for zones with very different requirements. In that case, the website at http://www.nct.rip/docs/195-re-204.html is recommended reading.

### The Zone File's Other Records

The next two lines in the zone file create NS and PTR records. The NS record has no explicit name specified, so it uses the last one, which is the @ of the SOA record. Thus, the nameserver for 0.0.127.in-addr.arpa is defined to be localhost.

The PTR record has the name 1, which becomes 1.0.0.127.in-addr.arpa (which is how you write the address 127.0.0.1 as a DNS name). When qualified, the PTR record name 1 becomes localhost. (You will see some of the numerous other RR types later when we configure our nameserver to be authoritative for a real domain.)

## TXT RECORDS AND SPF

One record not already mentioned is the TXT record. This record is usually used for documentation purposes in DNS, but a recent proposal uses the TXT record to help in the fight against email address forgery, spam, and phishing attacks.

One problem with email and SMTP is that when email is being delivered, the sender can claim that the email is coming from trusted.bank.com, when really it is coming from smalltime.crook.com. When the recipient of the email gets the email, it looks like valid instructions from trusted.bank.com, but if the receiver trusts the email and follows its instructions, his bank accounts can become vulnerable. These situations can be controlled by using SPF (*Sender Policy Framework*).

Domains can publish the valid IP address of their email servers in specially formatted TXT records. A TXT record could look like this:

```
trusted.bank.com. IN TXT "v=spf1 ip4:37.21.50.80 -all"
```

This record specifies that only one IP address is allowed to send mail for trusted.bank.com. Receiving email servers can then do one extra check with incoming email. When an email arrives, they know the IP address that the email is coming from. They also know that the sender claims to be coming from trusted.bank.com, for example. The receiving email server can look up the DNS TXT record for trusted.bank.com, extract the allowed IP addresses, and compare them to the IP address that the email really is coming from. If they match, it is an extremely good indication that the email really is coming from trusted.bank.com. If they do not match, it is a very good indication that the email is bogus and should be deleted or investigated further.

The SPF system does rely on cooperation between senders and receivers. Senders must publish their TXT records in DNS, and receivers must check the records with incoming email. If you want more details on SPF, visit the home page at http://spf.pobox.com/.

## Logging

We now have all the elements of a minimal functioning DNS server, but before we experiment further, some extra logging will allow us to see exactly what named is doing. Log options are configured in a logging section in named.conf, and the various options are described in detail in the BIND 9 ARM.
