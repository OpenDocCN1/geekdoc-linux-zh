Thus, for example, if *shishi* were running a local name server, it would quickly build up a cache of answered queries. Eventually, *shishi* would directly answer most queries, with only occasional queries being sent out over the Internet.

Of course, answers to DNS queries cannot be cached forever—if a host’s IP changes, the cached results are invalid. For that reason, the authoritative servers for a query specify a “time to live” for the query’s answer. If the answer to a query is cached for longer than its time to live, the cached result is invalidated and the authoritative server is queried.

# Background Material

This is why when a machine’s IP address changes, it may take hours or days for the change to propagate across the worldwide DNS. All the cached entries have to expire.

# DNS Record Types

All DNS queries have a type and the answers have a corresponding record type. Each answer is called a *resource record* or RR for short. Here are some DNS RR types:

+   *   A	An A-type record contains the IP address of a host. This record type is queried most often.
+   *   CNAME	A CNAME-type record holds a host’s canonical name. For example, many organizations name their Web server *www*. However, this is usually just a nickname for the real Web server. If your Web server’s real name is *bigserver.roaringpenguin.com*, you can create a CNAME record for *www.roaringpenguin.com*, which lists *bigserver.roaringpenguin.com* as the canonical name. If you ever have to move the Web server to a different machine, you need only change the CNAME record.
+   *   MX	An MX-type record holds the machine used for mail exchange. For example, the machine handling mail for *roaringpenguin.com* might be called *mail.roaringpenguin.com*.
+   *   NS	An NS-type record lists the name servers used for a domain. For example, the name servers for *roaringpenguin.com* are *dns.storm.ca* and *sns.storm.ca*.
+   *   PTR	A PTR-type record is used for reverse DNS—that is, given an IP address, find the host name corresponding to the IP address.
+   *   SOA	An SOA-type record holds the start-of-authority information for a domain. This includes the e-mail address of the person responsible for the DNS domain as well as various time-to-live and timeout values.

There are other DNS record types, but the ones described above are the most common.