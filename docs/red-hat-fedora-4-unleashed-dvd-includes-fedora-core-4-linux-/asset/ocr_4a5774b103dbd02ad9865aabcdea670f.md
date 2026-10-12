value of one or two weeks is too short. One thousand hours (about six weeks) is accepted as a good default.

As you read earlier, every RR has a TTL, which specifies how long it can be cached before the origin of the data must be consulted again. If the RR definition does not specify a TTL explicitly, the default TTL (set by the $TTL directive) is used instead. This enables individual RRs to override the default TTL as required.

The SOA TTL, the last numeric field in the SOA record, is used to determine how long negative responses (NXDOMAIN) should be cached. (That is, if a query results in an NXDOMAIN response, that fact is cached for as long as indicated by the SOA TTL.) Older versions of BIND used the SOA minimum TTL to set the default TTL, but BIND 9 no longer does so. The default TTL of 2 days and SOA TTL of 1 hour is recommended for cache friendliness.

The values used previously are good defaults for zones that do not change often. You might have to adjust them a bit for zones with very different requirements; in which case, the website http://www.ripe.net/docs/ripe-203.html is recommended reading.

# The Zone File’s Other Records

The next two lines in the zone file create NS and PTR records. The NS record has no explicit name specified, so it uses the last one, which is the @ of the SOA record. Thus, the nameserver for 0.0.127.in-addr.arpa is defined to be localhost.

The PTR record has the name 1, which becomes 1.0.0.127.in-addr.arpa (which is how you write the address 127.0.0.1 as a DNS name). When qualified, the PTR record name 1 becomes localhost. (You will see some of the numerous other RR types when we later configure our nameserver to be authoritative for a real domain.)

# TXT Records and SPF (Sender Policy Framework)

One record not already mentioned is the TXT record. This record is usually used for documentation purposes in DNS, but a recent proposal is using the TXT record to help in the fight against email address forgery, spam, and phishing attacks.

One problem with email and SMTP is that when email is being delivered, the sender can claim that the email is coming from trusted.bank.com, when it really is coming from smalltime.crook.com. When the recipient of the email gets the email, it looks like valid instructions from trusted.bank.com, but if they do trust the email and follow the instructions, their bank accounts can become vulnerable.

These situations can be controlled by using SPF.

Domains can publish the valid IP address of their email servers in specially formatted TXT records. A TXT record could look like this:

```
trusted.bank.com. IN TXT "v=spf1 ip4:37.21.50.80 -all"
```

This record specifies that only one IP address is allowed to send mail for trusted.bank.com.

Receiving email servers can then do one extra check with incoming email. When an email arrives, they know the IP address that the email is coming from. They also know that the sender claims to be coming from trusted.bank.com, for example. The receiving email server can look up the DNS TXT record for trusted.bank.com, extract the allowed IP addresses, and compare them