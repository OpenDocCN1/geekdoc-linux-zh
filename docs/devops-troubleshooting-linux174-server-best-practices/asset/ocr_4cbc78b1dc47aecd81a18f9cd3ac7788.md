DNS lookups on the command line, this would be apparent when you try to load a new website in a browser and it lags for about 30 seconds before it loads.

If you suspect that one of your recursive DNS servers is down, confirming the suspicion is pretty straightforward. Go through the list of name servers configured for your host (listed in /etc/resolv.conf on Linux) and perform DNS client troubleshooting, as discussed at the beginning of the chapter, to see if your list of name servers are up and replying. Basically, use nslookup to attempt to resolve a few well-known and presumably stable sites like www.google.com and www.yahoo.com, only make sure to add the IP address of the name server you want to test after the query, like so:

```
$ nslookup www.google.com 10.1.1.4
Server:\t10.1.1.4
Address:\t10.1.1.4#53

Non-authoritative answer:
www.google.com\tcanonical name = www.l.google.com.
Name:\twww.l.google.com
Address:\t74.125.224.144
Name:\twww.l.google.com
Address:\t74.125.224.145
Name:\twww.l.google.com
Address:\t74.125.224.146
Name:\twww.l.google.com
Address:\t74.125.224.147
Name:\twww.l.google.com
Address:\t74.125.224.148
```

If you follow the steps from the DNS client troubleshooting section, you should be able to tell whether the DNS server is up and reachable or not. Once that’s confirmed, and you still can’t resolve sites, you might see an error like the following:

```
$ nslookup www.example.net 10.1.1.4
Server:\t10.1.1.4
Address:\t10.1.1.4#53

** server can't find www.example.net: REFUSED
```