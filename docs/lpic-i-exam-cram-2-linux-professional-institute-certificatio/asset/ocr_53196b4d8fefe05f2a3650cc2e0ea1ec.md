# The named.* Files

The following is an example of the two files—/etc/named.boot for BIND v4 and /etc/named.conf for BIND v8:

Example of BIND v4 /etc/named.boot file:

```
# bind configuration file
directory /usr/local/named
primary	somecoll.edu	db.somecoll
primary	33.168.192.in-addr.arpa	db.33.168.192
primary	0.0.127.in-addr.arpa	db.0.0.127
cache	db.cache
```

The version 4 file is simple and direct, beginning with a comment and then getting into the configuration.

The lines in this file define the following, in order:

+   ▸ directory—The directory that contains the configuration files mentioned in the following lines.

+   ▸ primary—The first primary entry defines this server as the primary or master server for the somecoll.edu domain; then it references the actual zone file (db.somecoll.edu) where zone information is kept.

+   ▸ primary—The second primary entry defines the reverse lookup for the zone that uses network 192.168.33.0.

+   ▸ primary—The final primary entry defines a local 127.0.0.0 reverse lookup zone, a common part of most configurations.

+   ▸ cache—This entry defines that the cache for the server exists and is named db.cache.

When you know what’s in the file and how it looks, you’re ready to compare it with the v8 file.

Here’s an example of the BIND v8 /etc/named.conf file:

```
// bind configuration file
options {
	directory "/usr/local/named";
};
zone "somecoll.edu" in {
	type master;
	file "db.somecoll";
}
```