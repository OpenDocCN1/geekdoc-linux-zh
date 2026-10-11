```
zone "33.168.192.in-addr.arpa" in {
    type master;
    file "db.33.168.192";
}
zone "0.0.127.in-addr.arpa" in {
    type master;
    file "db.0.0.127";
}
```

The BIND v8 file is more complex and has a lot more formatting, appearing more like a C or C++ file source file than the plain-text keyword/value entries in the v4 configuration file.

Rather than put you through a line-by-line comparison, suffice it to say that where you would use a single-line entry in a v4 file, the v8 file uses blocks defined by a keyword such as options or zone and a set of parameters completely encased in curly brackets as the value for the keyword.

![](bbox=[0.11, 0.39, 0.24, 0.47])

> Expect to see one or the other of these files in your exam experience, with various questions about what the role of the server is and which networks the zones might be serving. A careful inspection of the examples will tell you all you need to know for the exam, and more.

# Zone and Record Types

A *zone* is an organization unit that is similar to a domain. A quick run-through of the various types of zones will help you determine what the role of a server is:

+   - **Master**—A master zone contains the information needed to resolve the hostnames to IPs and is considered an authority on the domain.
+   
+   - **Slave**—A slave zone is a copy or replica of a master zone and is used for traffic management or load balancing. It can only receive zone information from a master, not update a master.
+   
+   - **Forward**—This zone type simply points to another server, typically an ISP or a higher-echelon corporate DNS server for resolution; it doesn't do any resolution itself.
+   
+   - **Hint**—A hint zone is used to locate a root server so a query that is not resolvable by the local servers can be resolved.

BIND uses several resource record types. The one you're most likely familiar with is an A, or address, record, which is simply a hostname and IP record.