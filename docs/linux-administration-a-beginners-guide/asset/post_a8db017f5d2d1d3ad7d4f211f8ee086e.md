
# 251

# Chapter 12: DNS

name server would understand it to be oid.planetoid.org. So if you want to use the FQDN, be sure to suffix it with a period.

### PTR: Pointer Record

The PTR record is for performing reverse name resolution, thereby allowing someone to specify an IP address and determine the corresponding host name. The format for this record is very similar to the A record, except with the values reversed:

![](img/95b125a8bf06051f34d8aba73558b7eb_282_0.png)

The *IP-address* can take one of two forms: just the last octet of the IP address (leaving the name server to automatically suffix it with the information it has from the in-addr.arpa domain name), or the full IP address, which is suffixed with a period. The *host name* must have the complete FQDN. For example, the PTR record for the host oid would be as follows:

![](img/95b125a8bf06051f34d8aba73558b7eb_282_1.png)

### MX: Mail Exchanger

The MX record is in charge of telling other sites about your zone’s mail server. If a host on your network generated an outgoing mail with its host name on it, someone returning a message would not send it back directly to that host. Instead, the replying mail server would look up the MX record for that site and send the message there instead.

When Internet sites were primarily composed of UNIX-based systems, with Sendmail configured as a NULL host forwarding to a mail hub, lack of an MX record was okay. But as more non-UNIX systems joined the Net, MX records became crucial. If pc.domain.com sends a message using its PC-based mail reader (which cannot accept SMTP mail), it’s important that the replying party have a reliable way of knowing the identity of pc.domain.com’s mail server.

The format of the MX record is as follows:

![](img/95b125a8bf06051f34d8aba73558b7eb_282_2.png)

where *domainname*, is the domain name of the site (with a period at the end, of course); the *weight* is the importance of the mail server (if multiple mail servers exist, the one with the smallest number has precedence over those with larger numbers); and the *host name* is of course the name of the mail server. It is important that the *host name* have an A record, as well.

Here’s an example entry:

```
domain.com.    IN MX 10 mailserver1
           IN MX 20 mailserverbackup
```

Typically, MX records occur at the top of DNS configuration files. If a domain name is not specified, the default name is pulled from the SOA record.

### CNAME: Alias Record

CNAME records allow you to create aliases for host names. This is useful when you want to provide a highly available service with an easy-to-remember name, but still give the host a real name.

Another popular use for CNAMEs is to “create” a new server with an easy-to-remember name without having to invest in a new server at all. An example: A site has a mail server named mailhost in a UNIX-like tradition. As non-UNIX people come into the Internet picture, they assume the mail server will be called mail; to accommodate this assumption, a CNAME is created rather than renaming the server, so that all requests to the host named mail will transparently resolve to mailhost.

Here’s the format for the CNAME record:

```
newhost name IN CNAME oldhost name
```

For example, for the mail-to-mailhost mapping mentioned just above, our entries might look like this:

```
mailhost IN A 192.168.1.10
mail IN CNAME mailhost
```

> WARNING: It’s a bad, bad, bad practice to point an MX record to a CNAME record. The official DNS specification document explicitly prohibits this. BIND will allow it, but only to keep backward compatibility with a broken feature from the past.

### RP and TXT: The Documentation Entries

Sometimes it’s useful to provide contact information as part of your database—not just as comments, but as actual records that others can query. This can be accomplished using the RP and TXT records.

TXT records are a free-form text entry into which you can place whatever information you deem fit. Most often, you’ll only want to put contact information in these records. Each TXT record must be tied to a particular host name. For example:

```
hhgtg.planetoid.org. IN TXT “Contact: Marvin”
IN TXT “SysAdmin/Android”
IN TXT “Voice: 800-555-1212”
```

The RP record was created as an explicit container for a host’s contact information. This record states who is the responsible person for the specific host; here’s an example:

```
hhgtg.planetoid.org. IN RP marvin.domain.com. planetoid.org.
```

### PUTTING IT ALL TOGETHER

So now we have the entries we need in the /etc/named.conf file, and we know about all the DNS record types. It’s time to create the actual database that will feed the server.

The database file format is not too strict, but some conventions that have jelled over time. Sticking to these conventions will make your life easier and will smooth the way for the administrator who takes over your creation.

> **TIP:** Comment liberally. In this file, comment lines begin with a semicolon. Although there isn't a lot of technology about what's going on in a DNS database file, a history of the changes is a useful reference about what was being accomplished and why.

Every database file must start with an SOA record and contain at least one NS record. Everything else is optional. (Of course, "everything else" is what makes the file useful!) You may find the following general format helpful to follow:

```
SOA record
NS records
MX records
A and CNAME records
```

For example, here is a complete zone configuration file for a single domain with four hosts:

```
@ IN SOA domain.com. hostmaster.domain.com. (
    1999022300 ; serial number
    10800 ;Refresh every 3 hours
    1800 ;Retry every 30 minutes
    1209600 ;Expire in 2 weeks
    604800 ) ;Minimum 1 week
    IN NS ns.domain.com.
    IN MX 10 mail.domain.com.
imp IN A 192.168.1.1 ; Internet gateway
mail IN A 192.168.1.2 ; mail server
techies IN A 192.168.1.3 ; web server
www IN CNAME techies
ns IN A 192.168.1.4 ; name server
peanutbutter IN A 192.168.1.5 ; firewall
```

And here is the corresponding reverse file:

```
@ IN SOA 1.168.192.in-addr.arpa. hostmaster.domain.com. (
    1999010501 ; Serial
    10800 ; Refresh rate (3 hours)
    1800 ; Retry (30 minutes)
    1209600 ; Expire (2 weeks)
    604800 ) ; Minimum (1 week)
    IN NS ns.domain.com.
1 IN PTR imp.domain.com.
2 IN PTR mail.domain.com.
3 IN PTR techies.domain.com
4 IN PTR ns.domain.com
5 IN PTR peanutbutter.domain.com.
```

### A Complete Configuration

So far we’ve given you snippets of configuration files. Hopefully that has been enough to give you the big DNS picture and provide plenty of guidance for coming up with your own configuration file. Then again, a nice example never hurts.

Following is a complete configuration for a primary domain (domain.com) that also acts as a secondary to a friend, example.com. In exchange, the example.com domain acts as our secondary. We allow zone transfers to occur between our two sites, but not with any other sites. The domain.com site’s ISP provides DNS service, as well, to which we forward requests when we cannot resolve information ourselves.

Here is the /etc/named.conf file:

```
options {
	directory "/var/named";
	forwarders {
		192.168.2.1;
		192.168.2.2;
	};
	allow-transfer { 10.0.0.1; 10.0.0.2; }  // the example.com name servers
};

//
// a caching only name server config
//
zone ".*" {
	type hint;
	file "named.ca";
};

zone "0.0.127.in-addr.arpa" {
	type master;
	file "named.local";
};

//
// our primary information
//
zone "domain.com" {
	type master;
	file "named.domain.com";
};

zone "1.168.192.in-addr.arpa" {
    type  master;
    file  "named.rev";
};

//
// our secondary information for example.com
//
zone "example.com" {
    type  slave;
    file  "example.com.cache";
    masters { 10.0.0.1; 10.0.0.2; };
};
```

Here is the /var/named/named.ca file:

```
;  This file holds the information on root name servers needed to
;  initialize cache of Internet domain name servers
;  (e.g. reference this file in the `cache   .file`
;  configuration file of BIND domain name servers).
;
;  This file is made available by InterNIC registration services
;  under anonymous FTP as
;
;          file            /domain/named.root
;          on server       FTP.RS.INTERNIC.NET
;          -OR- under Gopher at  RS.INTERNIC.NET
;
;          under menu      InterNIC Registration Services (NSI)
;              submenu     InterNIC Registration Archives
;                  file    named.root
;
;          last update:     Aug 22, 1997
;          related version of root zone: 1997082200
;
;  formerly NS.INTERNIC.NET
;
.
```
