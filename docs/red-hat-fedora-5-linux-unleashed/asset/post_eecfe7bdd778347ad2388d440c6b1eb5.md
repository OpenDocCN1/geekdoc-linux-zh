
```
zone "foo.example.com" {
    type slave;
    file "foo.example.com";
    masters {
        192.0.2.96;
    };
}
```

Similarly, our friend must configure 192.0.2.96, which is a master for foo.example.com and a slave for example.com. She must also configure her server to accept mail addressed to example.com. Usually, mx2 would just queue the mail until it could be delivered to mx1.

## Reverse Zone

Let us pretend that we live in a perfect world: Our highly competent ISP has successfully delegated authority of our reverse zone to us, and we must set up named to handle reverse resolution as well. This process is very similar to what you used to set up the reverse zone for 0.0.127.in-addr.arpa. Now, however, you must determine your zone's name.

DNS can only delegate authority at the "." in domain names; as a result, you can set up reverse zones for the whole of a class A, B, or C network because they are divided at octet boundaries in the IP address. This approach is clearly unsuitable for classless subnets such as ours because the divisions are not at octet boundaries, but in the middle of an octet. In other words, our network cannot be described as x.* (class A), x.y.* (class B), or x.y.z.* (class C). The latter comes closest, but includes several addresses (such as 192.0.2.22) that do not belong to our tiny 192.0.2/29 network. To set up a reverse zone for our network, we must resort to the use of classless delegation (described in RFC 2317).

The ISP, which is authoritative for the 2.0.192.in-addr.arpa zone, must either maintain your reverse zone for you or add the following records into its zone file:

```
1       CNAME   1.1-6
2       CNAME   2.1-6
3       CNAME   3.1-6
4       CNAME   4.1-6
5       CNAME   5.1-6
6       CNAME   6.1-6

1-6     NS      192.0.2.1
1-6     NS      192.0.2.96
```

The first `CNAME` record says that `1.2.0.192.in-addr.arpa` is an alias for `1.1.6.2.0.192.in-addr.arpa.` The others are similar. We do not have `CNAMEs` for network and broadcast addresses `0` and `7` because they do not need to resolve. Resolvers already know how to follow `CNAME` aliases while resolving names. When they ask about the `1.6` domains, they find the `NS` records defined previously and continue with their query by asking our nameserver about `1.1.6.2.0.192.in-addr.arpa.`

So, we must set up a zone file for `1.6.2.0.192.in-addr.arpa.` Apart from the peculiar name, this zone file is similar in every respect to the reverse zone we set up earlier, and should contain six `PTR` records apart from the `SOA` and `NS` records. Note that we make `192.0.2.96 (ns2)` a slave for the reverse zone as well, so the administrator must add a suitable zone statement to `named.conf` for it.

> **CAUTION**
> Be aware that, in the real world, you might have to wait for months for your ISP to get the reverse delegation right, and your reverse zone remains broken until then.

## Registering the Domain

You now have a working DNS setup, but external resolvers cannot see it because there is no chain of delegations from the root nameservers to yours. You need to create this chain by registering the domain, that is, by paying the appropriate registration fees to an authority known as a `registrar`, which then delegates authority over the chosen zone to your nameservers.

Nothing is magical about what a registrar does. It has authority over a certain portion of the DNS database (say the `com.` top-level domain [`TLD`]), and, for a fee, it delegates authority over a subdomain (`example.com`) to you. This delegation is accomplished by the same mechanisms that were explained earlier in our delegation of `foo.example.com.`

The site http://www.iana.org/domain-names.htm contains a list of all the TLDs and the corresponding registrars (of which there are now several). The procedure and fees for registering a domain vary widely between them. Visit the website of the registrar in question and follow the procedures outlined there. After wading through the required amounts of red tape, your domain should be visible to the rest of the world.

Congratulations! Your job as a DNS administrator has just begun.

## Troubleshooting DNS

Several sources offer good information about finding and fixing DNS errors. The DNSRD Tricks and Tips page at http://www.dns.net/dnsrd/trick.html and the `comp.protocols.tcp-ip.domains` FAQ (an HTML version is located at http://www.intac.com/~cdp/cptd-faq/1) are good places to start. This section discusses some of the more common errors and their cures.

> **NOTE**
>
> RFC 1912, “Common DNS Operational and Configuration Errors,” discusses several of the most common DNS problems at length. It is available at http://www.intac.com/~cdp/cpdt-faq/.

### Delegation Problems

Your zone must be delegated to the nameservers authoritative for them, either by the root nameservers or the parents of the zone in question. Improper delegation can cause the name service for your domain to become dysfunctional, prevent some networks from using the name service, and numerous other problems. These problems typically occur only in the initial stages of setting up a domain when the delegations have not propagated widely yet.

If you experience such problems, you can use `dig` to follow delegation chains and find the point at which problems occur. A tool such as `dnswalk` might also be useful (see “Tools for Troubleshooting,” later in this chapter).

Lame delegation is another common DNS delegation problem. *Lame delegation* occurs when a nameserver is listed as being authoritative for a zone, but in fact is not authoritative (it has not been configured to be a master for the zone); the nameserver in a lame delegation is called a *lame server*. Unfortunately, lame delegations are very common on the Internet. They can be the temporary result of domains being moved or (especially in the case of reverse zones) more permanent configuration errors that are never detected because of a lack of attention to detail.

If your registrar’s bills for your domain are not promptly paid, the registrar might discontinue the delegation of authority for your zone. If this happens (and the whois record for your domain usually mentions this), the best thing to do is quickly pay the registrar and ask for a renewal of the delegation. It is better not to let it happen, though, because such changes can take a relatively long time to make and propagate.

### Reverse Lookup Problems

Reverse lookup problems are often very hard to diagnose because they manifest themselves as failures in systems other than DNS. Many security-sensitive services perform reverse lookups on the originating host for all incoming connections and deny the connection if the query fails.

Even if reverse resolution succeeds, many servers might reject connections from your host if your `A` and `PTR` records do not match. That is, the `PTR` record for a particular `IP` address refers to a name and the `A` record for that name refers to a different `IP` address. They perform a double lookup to verify that the `PTR` and `A` records match to eliminate spoofing attacks. Carefully maintain your reverse zones at all times.

Delegation problems are a frequent source of woe. Unfortunately, many ISPs appear unable to understand, configure, or delegate reverse zones. In such cases, you often have

![](img/2045828cf45e5632bf056f9ca99d6755_766_0.png)

little choice but to try and tell your ISP what to do to fix the problem. If the ISP staff refuses to listen, find a new ISP (or live with broken DNS). Another typical symptom of failing reverse lookups is an abnormally long delay on connection attempts. This happens when the server's query for a PTR record is not answered and times out (often because of network problems or the nameserver being down). This can be baffling to diagnose, but you should suspect DNS problems whenever you hear questions such as “Hey! Why is my web browser taking so long to connect?”

### Maintaining Accurate Serial Numbers

Accurate serial numbers are very important to the correct operation of slave servers. An increase in the serial number of a zone causes slaves to reload the zone and update their local cache.

A common mistake that system administrators make is forgetting to increment the serial number after a change to the zone data. If you make this mistake, secondary nameservers won't reload the zone, and continue to serve old data. If you suspect that the data on the master and slave servers is out of sync, you can use dig to view the SOA record for the zone on each server `dig @master domain SOA` and `dig @slave domain SOA` and compare the serial numbers in the responses.

Another common problem is setting the serial number to an incorrect value—either too small or too large. A too-small serial number causes slaves to think that they possess a more up-to-date copy of the zone data, but this is easily corrected by increasing the serial number as necessary. A too-large serial number is more problematic and requires more elaborate measures to repair.

Serial number comparisons are defined in such a way that if a serial number—when subtracted from another with no overflow correction—results in a positive number, the second number is newer than the first, and a zone transfer is required. (See RFC 1982 “Serial Number Arithmetic” for details.) You can exploit this property by temporarily setting the serial number to 2¹⁶ (4,294,967,296), waiting for all the slaves to reload the zone, and then setting it to the correct number.

### Troubleshooting Problems in Zone Files

The most common error in zone data is to forget that names in a zone file are relative to the origin of the zone, not to the root. Writing www.example.com in the zone file for example.com and expecting it to be fully qualified causes names such as www.example.com.example.com to show up in the DNS. You should either write www, which is qualified to the correct www.example.com, or write www.example.com. (with the trailing period) to indicate that the name is fully qualified.

The SOA record should contain (as the first field) the domain name of the master server (not a CNAME) and a contact address (with the @ replaced by a ".") to report problems to. Mail sent to this address should be read frequently. The other fields should contain sensible values for your zone, and the serial number should be correctly incremented after each change.
