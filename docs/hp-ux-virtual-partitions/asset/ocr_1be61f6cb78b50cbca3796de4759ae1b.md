```
Oct 12 09:21:34 stimpv named[1893]: secondary zone "1.1.10.IN-AD-
DR.ARPA" loaded (serial 1)

Oct 12 09:21:35 stimpv named[1893]: secondary zone "baseball.hp.com"
loaded (serial 1)

Oct 12 09:21:35 stimpv named[1893]: secondary zone "2.1.10.IN-AD-
DR.ARPA" loaded (serial 1)

Oct 12 09:21:35 stimpv named[1893]: secondary zone "1.168.192.IN-AD-
DR.ARPA" loaded (serial 1)

Oct 12 09:21:35 stimpv named[1893]: secondary zone "3.1.10.IN-AD-
DR.ARPA" loaded (serial 1)

Oct 12 09:21:36 stimpv named[1893]: secondary zone "2.168.192.IN-AD-
DR.ARPA" loaded (serial 1)

Oct 12 09:21:36 stimpv named[1893]: secondary zone "3.168.192.IN-AD-
DR.ARPA" loaded (serial 1)
```

Notice the serial number entries. They should match on the Master (primary) and Slaves (secondaries).

# ## A Word on Cache-Only Name Servers

Why in the world would you want a cache-only name server? In a word, performance. If you want to maintain a local cache but do not want to manage database files, this is the way to go. It will act as any other name server, responding to queries in the same fashion, except queries that are built in the cache will be non-authoritative. Any query that comes back with a non-authoritative reply is a query received from cache. Is that a bad thing? No, but be aware that the data may have changed on the Master (primary) and the cache replies may be outdated. The Time To Live (TTL) flag for each query is a way to manipulate the time, in seconds, that a name server may cache the answer to a query, versus having to contact an authoritative name server. The default TTL for records is usually 86400 seconds, or 24 hours. You may want to play with this value, depending on how frequently or infrequently the records are updated. A good rule of thumb is to have at least one name server per subnet, and cache-only name servers are an excellent choice.