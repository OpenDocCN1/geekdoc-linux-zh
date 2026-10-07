# Providing DNS for a Real Domain

(class C). The latter comes closest, but includes several addresses (such as 192.0.2.22) that don't belong to our tiny 192.0.2/29 network. To set up a reverse zone for our network, we must resort to the use of classless delegation (described in RFC 2317).

The ISP, which is authoritative for the 2.0.192.in-addr.arpa zone, must either maintain your reverse zone for you, or add the following records into its zone file:

```
| | |
| 1 CNAME 1.1-6 |
| 2 CNAME 2.1-6 |
| 3 CNAME 3.1-6 |
| 4 CNAME 4.1-6 |
| 5 CNAME 5.1-6 |
| 6 CNAME 6.1-6 |
|
 1-6 NS 192.0.2.1 |
| 1-6 NS 192.0.2.96
```

The first CNAME record says that 1.2.0.192.in-addr.arpa is an alias for 1.1-6.2.0.192.in-addr.arpa. (The others are similar. We don't have CNAME records for network and broadcast addresses and 7 because they don't resolve to.) Resolvers already know how to follow CNAME aliases while resolving names. When they ask about the 1-6 domain, they find the NS defined previously and continue with their query asking us name server about 1.1-6.2.0.192.in-addr.arpa.

So, we must set up a zone file for 1.1-6.2.0.in-addr.arpa. From the peculiar name, this zone file is similar in every respect to the reverse zone we set up earlier, and should contain six PTR records (apart from the SOA and NS records). Note that we 192.0.2.96 (n2) is a slave for the reverse zone as well, so the administrator must add a suitable zone statement to named.conf for.

> CAUTION
Be aware that in the real world you might have to wait for months for your ISP to get the reverse delegation right, and your reverse zone will remain broken until then.

# Registering the Domain

You now have a working DNS setup, yet external resolvers cannot see it because there is no chain of delegations from the root name servers to yours. You need to create this chain by registering the domain; that is, by paying the registration fee to an authority known as a registrar, who then delegates authority over the chosen zone to your name servers.