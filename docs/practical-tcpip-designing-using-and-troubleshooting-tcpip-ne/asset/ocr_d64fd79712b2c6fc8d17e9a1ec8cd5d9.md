# Summary

We have covered DNS problems only from a client perspective. We haven't covered problems with DNS servers, because we don't know what servers you're going to use, if any. However, the background we've given you will be of great benefit when you start using and configuring your own servers, and the symptoms of the problem as seen from the client will often give you a good pointer to what's going wrong on the server.

+   - the approach to take when troubleshooting DNS is first to identify the problem clearly, and then look for possible causes
+   - use `tcpdump` as soon as you suspect a problem. Look at the details of the queries your resolver is sending
+   - check the three fundamental networking parameters of your machine. Is it even successfully sending the queries to the DNS servers?
+   - check your machine's DNS configuration
+   - using `nslookup` or `host`, try the same resolution using a different nameserver
+   - use the debug options in `nslookup` or `host`
+   - is it really the DNS that's trying to resolve the name, or is another resolution system, and/or the `hosts` file, interfering? Again, `tcpdump` will let you see exactly what traffic your machine is sending.

# What's next?

That completes the DNS. We have all the basic networking infrastructure we need:

+   - we can communicate between two or more machines on a single wire, which lets us build small LANs
+   - we can use routers to interconnect separate networks and so build inter-networks of any size (including the Internet)
+   - we can refer to machines by name, not just by IP number, which is easier for human users (and also makes application's configuration files much clearer).

This is the end of Part 1 of the book, which in many ways is the hardest because there is so much low-level detail. In Part 2 we deal with applications – what the user really wants – where we work at a higher and less detailed level.

# Notes and further reading

On some very old versions of some operating systems, hostnames used for the “r-commands” (`rsh`, `rcp`, etc.; see Notes, Chapter 10) must be in `hosts` to be authorized, even if they can be resolved successfully using the DNS. However, that's now historical usage – you don't need it with NT or Linux.

In Module 9.1 we said there's a bug relating to authoritative answers. What can happen is that client Alice queries a nameserver, Dave say, for a name. Dave gets an authoritative answer,