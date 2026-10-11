Typically, the *ttl* and *class* portions are not used. However, you need to understand the full statement so that you can make your own decisions:

+   - *host*—The name of the machine you are defining. Often, this is just the hostname.
+   - *ttl*—The time to live value for this resource record—how long any resolver should keep this record in its cache before flushing it and asking for a new version.
+   - *class*—This value is always *IN* when you are setting up name service for TCP/IP purposes. Because it defaults to the last class used, and *IN* is the class in the SOA, you do not need to include this item.
+   - *IPaddress*—The IP address matching this host entry.

> NOTE: All terms used to define these records mean the same from type to type unless otherwise specified.

Next is the *CNAME* record. You assign a canonical name, or nickname, to a host in this format:

```
nickname ttl class CNAME host
```

The *nickname* is the alternate name you want to assign to this machine, whereas the *host* is the name of the machine you want to assign the *CNAME* to.

After this comes the *HINFO* record. Whether you choose to include information about the host's hardware or not is up to you. Some consider it a security risk, whereas others use it to keep track of large networks of different kinds of hardware. An alternative to this use is to use commented lines—beginning with a semicolon—to denote different segments of the network. A *HINFO* record is used in this format:

```
host ttl class HINFO hardware software
```

The *hardware* and *software* entries are strings of data. If these strings contain no spaces, then you do not need to put them in quotes. Otherwise, they need to be in double quotes.

A commonly used record type is the *MX* record, or mail exchange record. You enter this in the following format:

```
host ttl class MX preference mserver
```

Often, however, you only see the *MX, preference*, and *host* portions of this statement. The *host* part of the record refers to the machine whose preferences you