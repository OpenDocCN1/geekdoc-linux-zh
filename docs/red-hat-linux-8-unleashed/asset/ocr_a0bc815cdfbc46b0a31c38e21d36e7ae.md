Essential DNS Concepts

```
;; AUTHORITY SECTION:
200.203.addr.arpa. 86400 IN SOA dns.vsnl.net.in.
helpdesk.giasbm0.vsnl.net.in. 200001059 86400 7200 2592000 345600
```

```
;; Query time: 259 msec
;; SERVER: 203.197.12.42#53(ns3.vsnl.com.)
;; WHEN: Wed Sep 4 21:19:16 2002
;; MSG SIZE rcvd: 114
```

What happened? In previous responses, the status has always been NOERROR, but this has one status of NXDOMAIN (Nonexistent Domain), and the flags has the aa (Authoritative Answer) flag. This means that the name we are looking for is known not to exist. In contrast, the response from the root name servers didn't have the aa flag, and said "We don't know about this name: Ask someone else." The authoritative answer from ns3.vsnl.com says "I know this name does not exist, and why we may well looking."

The administrators at vsnl.net.in clearly haven't ever bothered to set up PTR records for their dual-up IP pool. If they had, the response would have looked like the ones we've seen before, and would have included a PTR record. As it is, the response lists the SOA record for zone including the email address of the domain contact, helpdesk@iasbm0.vsnl.net.in, should we choose to complain about broken reverse resolution.

# What Did the Resolver Solve?

We have a list of names and addresses of the authoritative name servers for the TLD. In the future, if we are asked to resolve, say.sampublishing.com, we can direct our query to tld-servers from the start of wasting one query on a root server. However, the NS records have an expiry time (also known as Time To Live, or TTL, which you learn about in "The Zone File," later in this chapter) of 2D, meaning that the information is guaranteed to answer for two days. For time updates is why you will see announcements made that it might take a few days for DNS changes to propagate throughout the Internet.

Similarly, we know the authoritative name servers for ibm.com, which are for use in queries involving ibm.com during the next two days. For instance, a Web browser will ask for the IP address of commerce.ibm when a user clicks on a link to the IBM Web page. We can save two queries by asking NS.WATSON.ibm.com in our cache, and we also have the four A records for www.ibm.com in that, and we can return one of them if the browser asks us to resolve the name again.

All this information (including that gleaned from the reverse resolution process) can be cached by your computer until expiry and to speed up further queries.

![](bbox=[0.935, 0.35, 0.995, 0.405])