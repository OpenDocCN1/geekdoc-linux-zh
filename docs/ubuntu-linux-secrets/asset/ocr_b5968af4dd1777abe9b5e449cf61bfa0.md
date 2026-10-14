# Table 20-3: (continued)

| Parameter | Description |
|---|---|
| -t querytype | Specify query type |
| -W wait | Wait for wait seconds for a response from the DNS server |
| w | Wait indefinitely for a response from the DNS server |
| -4 | Use only an IPv4 transport |
| -6 | Use only an IPv6 transport |

You can use the -l option to find information about all of the hosts listed in a domain. The -l option is often used with the -t option to filter particular types of information (such as -t MX, which returns all of the MX records for a domain). Unfortunately, in this day of security awareness it is often difficult to use the -l option because many DNS servers refuse attempts to access all of the host information contained in the database.

If you are trying to get information from a slow DNS server (or a slow link to the network) you may want to try the -w parameter. This parameter tells the host program to wait forever for a response to the query. By default, it will time out after about 1 minute.

One particularly useful parameter is -r, which tells the DNS server to return only information that it has in its own local DNS database regarding the query. The DNS server will not attempt to contact a remote DNS server to find the information.

The -r parameter is useful in determining whether your DNS server is properly caching DNS answers. First, try resolving a hostname using the -r parameter. If no one else has tried to resolve the hostname of this location, you should not get an answer back from your local DNS server.

Then try it without the -r parameter. You should get the normal DNS information back because the local DNS server was allowed to contact a remote DNS server to retrieve the information.

Next, try the host command again with the -r parameter. You should now get the same information that you received from the previous attempt. This means that the DNS server did indeed cache the results from the previous DNS query in its local name cache.

If you did not receive any information back, then your local DNS server did not cache the previous response. You should have noticed a significant decrease in the time it took to respond with an answer from cache compared to the response time after performing the DNS query on the network.

By default, the host command attempts to produce its output in human-readable format. Here's an example of a typical output:

```
$ host ubuntu.org
ubuntu.com has address 91.189.94.250
ubuntu.com mail is handled by 10 mx.canonical.com
```

If you specify a domain name, the host command automatically attempts to find the MX records associated with the domain.