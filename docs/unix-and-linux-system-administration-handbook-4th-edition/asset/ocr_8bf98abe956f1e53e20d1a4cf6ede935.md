have one-hour ttls. You can then be certain that all your updates will propagate together within an hour. Set the ttls back to their original value after you've completed your update campaign.

Some sites set the TTL on the records for Internet-facing servers to a low value so that if a server experiences problems (network failure, hardware failure, denial of service attack, etc.), the administrators can respond by changing the server's name-to-IP-address mapping. Because the original TTLs were low, the new values will propagate quickly. For example, the name google.com has a five-minute TTL, but Google's name servers have a TTL of four days (345,600 seconds):

```
google.com.      300 IN A   209.85.171.100
google.com.      345600 IN NS ns1.google.com.
ns1.google.com.  345600 IN A   216.239.32.10
```

We used the dig command to recover this data; the output is truncated here.

The class specifies the network type. Three values are recognized:

+   - IN for the Internet, which is the default
+   - HS for Hesiod, a directory service used locally by some sites
+   - CH, used internally by name servers to identify themselves

The default value for the class is IN. It is often specified explicitly in zone data files even though as the default, it can be omitted. Hesiod, developed at MIT, is a database service built on top of BIND.

CH originally stood for ChaosNet, a now-obsolete network protocol formerly used by Symbolics Lisp machines. Today, only two pieces of identification data are normally tucked away in the CH class: the version number of the name server software and the name of the host on which the server is running. These data nuggets can be extracted with dig or drill as shown on page 598.

Administrators and hackers use the name server version number to identify servers in need of upgrades, and admins use the host identification to debug name servers that are replicated through the use of anycast routing. Making this information available through the CH class was originally a feature of BIND, but the convention has now been adopted by other DNS implementations as well.

Many different types of DNS records are defined, but fewer than 10 are in common use; IPv6 adds a few more. We divide the resource records into four groups:

+   - Zone infrastructure records identify domains and their name servers.
+   - Basic records map between names and addresses and route mail.¹⁰
+   - Security records add authentication and signatures to zone files.
+   - Optional records provide extra information about hosts or domains.