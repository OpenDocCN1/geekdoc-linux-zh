# **LISTING 14.1** Example named.conf File

```
options {
	directory "/var/named";		# referred files in /var/named
};

zone "." {
	type hint;			# hints for caching
	file "named.ca";		# root servers file in
				# /var/named/named.ca
};

zone "0.0.127.in-addr.arpa" {	# reverse on loopback
	type master;
	file "named.local";
};

zone "100.168.192.in-addr.arpa" {	# reverse on eth0 subnet
	type master;			# file is on this host
	file "named.192.168.100";		# rev dns file
};

zone "domain.com" {			# DNS for all hosts this domain
	type master;			# file is on this host
	file "named.domain.com";		# dns file for domain
};
```

The options section holds information that's global to the entire DNS server. This one contains a single piece of information, the *directory* statement, which tells `named` the location of any filenames mentioned in the configuration.

`zone "."` is the caching zone. A caching zone isn't a master or slave, but rather a set of hints for the server software to use; hence the type `hints` statement. The file for zone `"."` is `named.ca`, which was created by Red Hat's installation. `named.ca` contains a list of all the root DNS servers on the Internet. These root servers are needed to prime `named`'s cache. You can get the latest list of root servers from the InterNIC at `ftp://rs.internic.net/domain/named.cache`.

Each zone has a type statement indicating master, slave, or hint and a *file* statement pointing to the file containing data for the zone. Files of type slave have a nested master section. This will be demonstrated in the section “Adding a Slave DNS Server” later in this chapter.

Each zone section defines a zone of authority, which is usually a domain, a subdomain or, in the case of reverse DNS, a subnet. Almost every zone defines a file from which it derives its information. Every zone has a type statement.