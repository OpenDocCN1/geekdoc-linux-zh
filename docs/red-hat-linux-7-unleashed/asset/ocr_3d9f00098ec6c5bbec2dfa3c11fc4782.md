In this example, the domain, domain.cxm, has two nameservers, ns1.domain.cxm, and ns2.domain.cxm.. These are fully qualified hostnames, so they need to have the period as the suffix. Without the period, named would evaluate their value to be ns1.domain.cxm.domain.cxm, which is not what you're looking for.

# A: Address Record

The address record is used for providing translations from hostnames to IP addresses. There should be an A record for each machine that needs a publicly-resolvable hostname. A sample entry using the A record is

```
mydesk    IN A        192.168.100.2
```

In this example, the address is specified for the host mydesk. Because this hostname is not suffixed by a period, named assumes it is in the same domain as the current SOA record. Thus, the hostname is mydesk.domain.cxm.

# PTR: Pointer Record

The pointer record, also known as the reverse resolution record, tells named how to turn an IP address into a hostname. PTR records are a little odd in that they should not be in the same SOA as your A records. Instead, they appear in an in-addr.arpa subdomain SOA.

A PTR record looks like this:

```
2.100.168.192.    IN PTR    mydesk.domain.cxm.
```

Notice that the IP address to be reverse-resolved is in reverse order and is suffixed with a period.

# MX: Mail Exchanger

The mail exchanger record enables you to specify which host on your network is in charge of receiving mail from the outside. sendmail uses this record to determine the correct machine to which mail needs to be sent. The format of an MX record looks like this:

```
domain.cxm.    IN MX 10    mailhub
                 IN MX 50    mailhub2
```

The first column indicates the hostname for which mail is received. In this case, it's domain.cxm. Based on the previous examples, you might have noticed that you have yet to specify a machine that answers to domain.cxm., but the sample MX record shows that you can accept mail for it. This is an important feature of DNS; you can specify a host-name for which you accept mail even if that hostname doesn't have an A record.