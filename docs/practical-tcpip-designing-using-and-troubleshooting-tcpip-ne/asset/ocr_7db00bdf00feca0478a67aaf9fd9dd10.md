# 9.1 Troubleshooting – identifying a problem

> **Tip:** you can often short-circuit the step-by-step troubleshooting approach below by running **tcpdump -n** immediately you get a DNS problem. After a while you’ll be able to get a good idea of what’s happening just from the **tcpdump**’s output, even though it is terse.

Some DNS difficulties you have might not be due to misconfiguration or network problems at your site:

+   1.a. the DNS can’t find the IP address for a name you’re trying to resolve because the name doesn’t exist. If you haven’t got any of the errors described below, you’ll see the status **NXDomain** (non-existent domain name) in the **tcpdump** trace:

```
192.0.2.17.3566 > 192.0.2.19.53: 19588 A? junk.example.com. (34)\n192.0.2.19.53 > 192.0.2.17.3566: 19588 NXDomain* 0/1/0 (95)
```

The application that requested the name resolution will report an error too. If the name resolution is deep inside the application, the application’s error message may not be clear. To make sure, run **host** or **nslookup** on the name that’s causing the problem and then you’ll get a clear message below. The cause could be either a typo on your part, or the name in question really doesn’t exist.

```
alice$ host junk.example.com\njunk.example.com does not exist (Authoritative answer)
```

Note that **host** said the answer was authoritative (and **tcpdump** indicated it was authoritative by printing its “\*” after NXDomain). That means that DNS really did go all the way through the delegations (for **ibm.com** in this example) and was told the name definitely doesn’t exist. This ought to assure you there were no other problems along the way (but there is a known bug in this area – see the Notes). The next module shows a typical failed resolution in full detail.

+   1.b. if DNS fails to resolve an internal name (which assumes you’re running your own DNS server for internal names) then maybe you do have a problem. For example, if you’re trying to resolve “alice” but you know Alice exists, a likely cause is that the domain-name and searchlist settings on our machine are empty. As a result DNS is trying to resolve the FQDN **alice.aice.example.com.** instead of, for example, **alice.example.com.**

+   1.c. or, it may be that internal machine Alice exists, but your site’s DNS administrator hasn’t entered the name **alice** in your DNS database. (Or your DNS server may be misconfigured in some other way.)

+   2. the DNS can’t find the name corresponding to an IP number, i.e. a reverse lookup fails. Unfortunately this is very common; frequently it’s because the DNS administrator for the site in question didn’t set up the PTR records properly. There’s nothing you can do about this

+   3. if you’re using Microsoft’s Internet Explorer (IE) browser, and a DNS lookup fails, IE itself caches the result. If the problem was caused by a problem with your DNS, even