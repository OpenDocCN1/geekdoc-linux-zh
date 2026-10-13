
The same name for multiple IP addresses can cause problems. For example, some services do not bind two addresses. They bind only one address. But which one? Normally, it will be the first one encountered. Likewise, clients looking to connect to that service sometimes connect and sometimes do not, depending on which IP address they get first in reference to their query. Such confusion needs to be avoided; you can only do so by assigning multi-homed hosts unique names to each IP address.

The final RR you’ll look at in this section is the MX, or mail exchange address. This RR takes a little more explanation. A sample MX record looks like the following:

```
bar.org.    IN    MX    50     foo.bar.org.
bar.org.    IN    MX    100    baz.bar.org.
```

The records read as follows: For mail being sent to user@bar.org, foo.bar.org is the primary mail host, and baz is the secondary mail host. The numbers 50 and 100 indicate the priority for the mail hosts. The lower the number, the higher the priority. The numbers can range from 0–65535, but in practice, the most common numbers tend to be 5, 10, 50, and 100 for simplicity’s sake. This allows MX hosts to be inserted before or after any existing entries without rewriting all the entries.

So if the primary mailhost is foo, but for whatever reason foo can’t receive an email message, baz receives it. But because our mail host is foo and that’s where folks receive their mail, what happens to mail delivered to baz? Well, baz checks the MX records too and sees that foo is the primary mail host, so baz tries to send to foo. If more MX records are found, baz looks at the hostname and priority. The host baz does not re-send mail to itself or an MX host with a higher or equal number; it only sends to those with a lower number. Eventually, though, foo comes back up and accepts the messages that baz has queued up (at least, we hope so).

The other RR types, HINFO, TXT, and WKS, are of little value to most sites, so they are not covered here. The important RRs for forward resolution have now been reviewed.

## Reverse Resolution Databases

Up to this point, you’ve looked at RRs for forward resolution db files. But sometimes a lookup is needed on a reverse resolution. That is, you have an IP address, but don’t know the host to which it belongs. Look at Listing 26.1, near the bottom of the listing, at the last two statements; the first refers to a localhost, and the substatements point to localhost.hosts. This is your forward resolution database. The next one, with a statement zone 127.in-addr.arpa, tells named that this is a reverse lookup statement and to use this on any lookup for an IP address beginning 127.x.x.x. If you are master for bar.org and have a zone bar.org with filename bar.org.hosts and the IP network is 192.168.0.0/24, your zone statement for the reverse resolution database is 0.168.192.in-addr.arpa. Your filename can be anything you want to call it—but 192.168.0.hosts is nice and descriptive.

The reverse resolution db file is slightly different from the forward resolution database, but only in the RRs used within. The SOA is very similar and might look like the following:

```
0.168.192.in-addr.arpa.    IN SOA foo.bar.org.  dab.bar.org. (
1998122301 10800 3600 604800 86400 )
```

The only difference here is the use of the backward network portion of the IP address corresponding to the domain, and the use of the `in-addr.arpa.` suffix. This special suffix is required on all RRs in the reverse resolution database.

The rest of the RRs in the database are of the following form:

```
1.0.168.192.in-addr.arpa.    IN PTR foo.bar.org.
2.0.168.192.in-addr.arpa.    IN PTR baz.bar.org.
```

These two entries are PTR records and point from the reversed IP address annotation with the `in-addr.arpa.` suffix to the host name. This file also carries the NS records in reverse form as follows:

```
0.168.192.in-addr.arpa.    IN NS foo.bar.org.
0.168.192.in-addr.arpa.    IN NS baz.bar.org.
```

Again, nothing unusual. The reverse address is that of the domain, just as the forward NS addresses were for the domain.

## named.root Database

The named.root database is a special database. This db file contains hints to the name server as to where to look for the root name servers on the Internet. Because these servers do change from time to time, this file also needs to be updated. A good rule of thumb for updating this is once a month. A script in the “dig” section that follows can be run to perform the update automatically.

## Name Server Tools

A number of tools that are useful for debugging DNS are available in Linux under the `bind-utils` and `whois` packages. These tools are invaluable to administrators. Although some overlap exists between the tools, each has its advantages and disadvantages. The best way to compare them is to take a look at some of them. This will also give you the opportunity to check your name server setup.

### nslookup

The nslookup program performs name server lookups. The program has two modes, interactive and non-interactive. Two ways are available to enter interactive mode. The first way is to run nslookup with no arguments. The second way is to run nslookup with a hyphen (signifying input from the keyboard) and a name server. If nslookup is not given a name server to use, it consults the `/etc/resolv.conf` file and uses the first one listed. If you are running a name server on your system, the first name-server line in `/etc/resolv.conf` should point to the localhost (127.0.0.1).

The nslookup program has eleven possible commands; two are the lookup name itself and the lookup name with a name server to use to perform the lookup. Other commands provide specific types of lookups or set options. The set command has 14 options that can be set. After they are set, these options remain in use until set is invoked to change them again.

The most common of the set arguments is to set the querytype. Query types can be any of the valid RR types plus a few extras (A, ANY, CNAME, HINFO, MX, PX, NS, PTR, SOA, TXT, WKS, SRV, NAPTR). The PX option provides information regarding zone creation, zone contact, serial number, and TTL information—just slightly less information than the SOA option. The ANY option provides PX information plus name servers, plus SOA. The SRV and NAPTR options provide information similar to the PX option, but specify the forward or reverse lookup databases respectively. The default is A.

When nslookup starts, it reports the DNS server that it will use for lookups and presents you with a prompt as follows:

```
bash-2.0$ nslookup
Default Server:   localhost
Address:  127.0.0.1
>
```

Each subsequent use reports the server again, so this information is omitted in subsequent examples.

Now, you’ll take a look at some output. First, look at the default output (querytype=A) for the domain calderasystems.com. The following is the non-authoritative answer:

```
Non-authoritative answer:
Name:  calderasystems.com
Address:  207.179.18.130
```

Note that the first line tells you that the answer you’ve obtained is non-authoritative. This means that the information was provided from information that the current DNS server cached.

Now look at the output after setting the querytype to ANY. Following is the non-authoritative answer:

```
calderasystems.com        nameserver = gw.caldera.com
calderasystems.com        nameserver = ns.calderasystems.com
calderasystems.com        internet address = 207.179.18.130
```

Authoritative answers can be found from:

```
calderasystems.com        nameserver = gw.caldera.com
calderasystems.com        nameserver = ns.calderasystems.com
gw.caldera.com  internet address = 207.179.18.252
ns.calderasystems.com  internet address = 207.179.18.7
```

Here again you see that the answer is non-authoritative. Following that, you see the name servers for the caldera.com domain listed. Then is the information from the SOA. Looking at the serial number, you can see that this is update 1 on 30 Jan 2000. Because this domain is maintained by someone other than the author of this chapter, you can see that the serial numbering convention I suggested earlier is a sound one from more than my point of view. Looking through the rest of this data, about the only information you don’t have is the MX data.
