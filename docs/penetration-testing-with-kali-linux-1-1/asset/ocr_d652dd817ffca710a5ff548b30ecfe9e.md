# 7.1.1 Interacting with a DNS Server

Each domain can use different types of DNS records. Some of the most common types of DNS records include:

+   - *NS* - Nameserver records contain the name of the authoritative servers hosting the DNS records for a domain.
+   - *A* - Also known as a host record, the "a record" contains the IP address of a hostname (such as www.megacorpone.com).
+   - *MX* - Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records.
+   - *PTR* - Pointer Records are used in reverse lookup zones and are used to find the records associated with an IP address.
+   - *CNAME* - Cannonical Name Records are used to create aliases for other host records.
+   - *TXT* - Text records can contain any arbitrary data and can be used for various purposes, such as domain ownership verification.

Due to the wealth of information contained within DNS, it is often a lucrative target for active information gathering.

To demonstrate this, we'll use the **host** command to find the IP address of www.megacorpone.com:

```
kali@kali:~$ **host www.megacorpone.com**
www.megacorpone.com has address 38.100.193.76
*Listing 210 - Using host to find the A host record for www.megacorpone.com*
```

By default, the host command looks for an A record, but we can also query other fields, such as MX or TXT records. To do this, we can use the -t option to specify the type of record we are looking for:

```
kali@kali:~$ **host -t mx megacorpone.com**
megacorpone.com mail is handled by 10 fb.mail.gandi.net.
megacorpone.com mail is handled by 50 mail.megacorpone.com.
megacorpone.com mail is handled by 60 mail2.megacorpone.com.
megacorpone.com mail is handled by 20 spool.mail.gandi.net.

kali@kali:~$ **host -t txt megacorpone.com**
megacorpone.com descriptive text "Try Harder"
*Listing 211 - Using host to find the MX and TXT records for megacorpone.com*
```

# 7.1.2 Automating Lookups

Now that we have some initial data from the megacorpone.com domain, we can continue to use additional DNS queries to discover more hostnames and IP addresses belonging to the same domain. For example, we know that the domain has a web server, with the hostname "www.megacorpone.com".

Let's run **host** against this hostname: