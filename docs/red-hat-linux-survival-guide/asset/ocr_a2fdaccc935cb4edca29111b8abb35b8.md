# Zone statement

Apart from the options statement, the zone statement is the only other type of statement that you find in virtually any site's named.conf configuration. To set up a name service for an Internet domain, you need to create a zone statement in the /etc/named.conf file. Three commonly used zone statements look as follows:

```
zone domain_name {
    type master;
    file path_name;
};
```

```
zone domain_name {
    type slave;
    masters { ip_addr; [ ip_addr; ... ] };
    file path_name;
};
```

```
zone "." {
    type hint;
    file path_name;
};
```

The first zone statement is used for a master (primary) zone. For example, if you want your name server to be the authoritative name server for a particular domain, you should set up a master zone. For example:

```
zone "ad-engine.com" {
    type master;
    file "ad-engine.db";
};
```

Here, the name server is configured as the primary name server for the ad-engine.com domain. Notice that the file option is used to specify the filename of the zone- or domain-specific configuration. If the filename you specify here is relative to the working directory of the server, it must reside inside the working directory.