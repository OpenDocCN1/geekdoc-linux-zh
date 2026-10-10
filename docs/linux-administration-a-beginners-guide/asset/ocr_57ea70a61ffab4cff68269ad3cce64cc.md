# 251

# Chapter 12: DNS

name server would understand it to be oid.planetoid.org. So if you want to use the FQDN, be sure to suffix it with a period.

# PTR: Pointer Record

The PTR record is for performing reverse name resolution, thereby allowing someone to specify an IP address and determine the corresponding host name. The format for this record is very similar to the A record, except with the values reversed:

![](bbox=[0.2, 0.37, 0.75, 0.39])

The *IP-address* can take one of two forms: just the last octet of the IP address (leaving the name server to automatically suffix it with the information it has from the in-addr.arpa domain name), or the full IP address, which is suffixed with a period. The *host name* must have the complete FQDN. For example, the PTR record for the host oid would be as follows:

![](bbox=[0.2, 0.55, 0.75, 0.57])

# MX: Mail Exchanger

The MX record is in charge of telling other sites about your zone’s mail server. If a host on your network generated an outgoing mail with its host name on it, someone returning a message would not send it back directly to that host. Instead, the replying mail server would look up the MX record for that site and send the message there instead.

When Internet sites were primarily composed of UN*X-based systems, with Sendmail configured as a NULL host forwarding to a mail hub, lack of an MX record was okay. But as more non-UN*X systems joined the Net, MX records became crucial. If pc.domain.com sends a message using its PC-based mail reader (which cannot accept SMTP mail), it’s important that the replying party have a reliable way of knowing the identity of pc.domain.com’s mail server.

The format of the MX record is as follows:

![](bbox=[0.2, 0.96, 0.7, 0.98])

where *domainname*, is the domain name of the site (with a period at the end, of course); the *weight* is the importance of the mail server (if multiple mail servers exist, the one with the smallest number has precedence over those with larger numbers); and the *host name* is of course the name of the mail server. It is important that the *host name* have an A record, as well.

Here’s an example entry:

```
domain.com.    IN MX 10 mailserver1
           IN MX 20 mailserverbackup
```

Typically, MX records occur at the top of DNS configuration files. If a domain name is not specified, the default name is pulled from the SOA record.