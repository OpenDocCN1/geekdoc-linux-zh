# Chapter 12. Berkeley Internet Name Domain (BIND)

+   - master — Designates the nameserver as authoritative for this zone. A zone should be set as the master if the zone's configuration files reside on the system.

+   - slave — Designates the nameserver as a slave server for this zone. Also specifies the IP address of the master nameserver for the zone.

+   - zone-statistics — Configures named to keep statistics concerning this zone, writing them to the default location (/var/named/named.stats) or the file listed the statistics-file option in the server statement. See Section 22.2.2 Other Statement Types for more information about the server statement.

# 12.2.1. Sample zone Statements

Most changes to the /etc/named.conf file of a master or slave nameserver involves adding, deleting zone statements. These zone statements can contain many options, most nameservers require only a small subset to function efficiently. The following zone statements are very basic examples illustrating a master-slave nameserver relationship.

The following is an example of a zone statement for the primary nameserver example.com (192.168.0.1);

```
zone "example.com" IN {
    type master;
    file "example.com.zone";n    allow-update ( none );
}
```

In the statement, the zone is identified as example.com, the type is set to master, and the named service is instructed to read the /var/named/example.com.zone file. It also named not to allow by any other hosts to update.

A slave zone statement for example.com looks slightly different from the previous example. For a slave server, the type is set to slave and in place of the allow-update line is a directive telling the IP address of the master server.

A slave zone statement for example.com may look like this:

```
zone "example.com" {
    type slave;
    file "example.com.zone";n    masters ( 192.168.0.1 );
}
```

This statement configures named on the slave server to look for the master server at the 192.168.0.1 IP address for the example.com zone. The information slave server receives from the master server is saved to the /var/named/example.com.zone file.

# 12.2.2. Other Statement Types

The following is a list of used statement types available within named.conf

+   - controls — Configures various security requirements necessary to use the rndc command to administer the named service.

See Section 12.4.1 Configuring /etc/named.conf to see how the controls statement look, including various options that may only be used with it.