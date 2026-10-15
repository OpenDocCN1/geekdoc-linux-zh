# Configuring a slave server for a zone

The zone statement for a slave is similar to that of a master:

```
zone "domain_name" {
    type slave;
    file "path";
    masters { ip_addr [port ip_port] [key keyname]; ... }; [no default]
    allow-query { address_match_list }; [any]
};
```

Slave servers normally maintain a complete copy of their zone’s database. The file statement specifies a local file in which the replicated database can be stored. Each time the server fetches a new copy of the zone, it saves the data in this file. If the server crashes and reboots, the file can then be reloaded from the local disk without being transferred across the network.

You shouldn’t edit this cache file, since it’s maintained by named. However, it can be interesting to look at if you suspect you have made an error in the master server’s data file. The slave’s disk file shows you how named has interpreted the original zone data—relative names and origin directives have all been expanded. If you see a name in the data file that looks like one of these

128.138.243.151.cs.colorado.edu.
anchor.cs.colorado.edu.cs.colorado.edu.

you can be pretty sure that you forgot a trailing dot somewhere.

The masters clause lists the IP addresses of one or more machines from which the zone database can be obtained. It can also contain the name of a masters list defined with a previous masters statement.

We have said that only one machine can be the master for a zone, so why is it possible to list more than one address? Two reasons. First, the master machine might have more than one network interface and therefore more than one IP address. It’s possible for one interface to become unreachable (because of network or routing problems) while others are still accessible. Therefore, it’s a good practice to list all of the master server’s topologically distinct addresses.

Second, named really doesn’t care where the zone data comes from. It can pull the database just as easily from a slave server as from the master. You could use this feature to allow a well-connected slave server to serve as a sort of backup master, since the IP addresses are tried in order until a working server is found. In theory, you can also set up a hierarchy of servers, with one master serving several second-level servers, which in turn serve many third-level servers.

# Setting up the root server hints

Another form of zone statement points named toward a file from which it can preload its cache with the names and addresses of the root name servers.