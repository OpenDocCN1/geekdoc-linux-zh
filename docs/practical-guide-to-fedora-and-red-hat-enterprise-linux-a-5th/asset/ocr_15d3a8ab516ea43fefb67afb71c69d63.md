# # A FULL-FUNCTIONED NAMESERVER

Because the IP addresses used in this example are part of the *private address space* (page 1100) you can copy the example and run the server without affecting global DNS. Also, to prevent contamination of the global DNS, each zone has the *notify* option set to NO. When you build a nameserver that is integrated with the Internet, you will want to use IP addresses that are unique to your installation. You may want to change the settings of the *notify* statements.

The *named.conf* file in this example limits the IP addresses that *named* answers queries from and sets up logging:

```
```text
$ cat /etc/named.conf
options {
    directory "/var/named";
    allow-query {127.0.0.1; 192.168.0.0/24;};;

zone "." IN {
    type    hint;
    file    "named.ca";};
zone "0.168.192.in-addr.arpa" IN {
    type    master;
    file    "named.local";
    notify  NO;
};

zone "sam.net" IN {
    type    master;
    file    "sam.net";
    notify  NO;
};

logging{
    channel "misc" {
        file "/var/log/bind/misc.log" versions 4 size 4m;
        print-time YES;
        print-severity YES;
        print-category YES;
    };
    channel "query" {
        file "/var/log/bind/query.log" versions 4 size 4m;
        print-time YES;
        print-severity NO;
        print-category NO;
    };
    category default {
        "misc";
    };
    category queries {
        "query";
    };
};
```
```