# 484 CONFIGURATION AND OPERATION OF A NAME SERVER

```
# host file excerpt for name server
options {
    directory "/etc/named";
}
# Rest Name-Server
zone "" {
    type hint;
    file "local.cache";
}
zone "example.org" {
    type master;
    file "named.hosts";
}
zone "0.0.0.127.in-addr.arpa {
    type master;
    file "named.local";
}
zone "192.192.168.in-addr.arpa" {
    type master;
    file "named.rev";
}
```

Listing 20.4 The file .etc/named.conf for a primary name server.

This file, like all other data files, is stored in standard Resource Record (RR) or Masterfile format. A detailed description of this format can be found in the BIND Operators Guide; an introduction is given in the following paragraphs.

The name server is a primary name server for the zone veggies.example.org. The database is located in the file named.hosts in the directory /var/named. In addition, the server is a primary name server for the zones 0.0.127.in-addr.arpa and 168.192.in-addr.arpa, which are used for 'reverse lookup'.

In the next step, the data of the individual computers whose zones are specified in the file /etc/named.conf must be entered in the corresponding files. The format of these files and the most important entries are explained in more detail on the following pages.