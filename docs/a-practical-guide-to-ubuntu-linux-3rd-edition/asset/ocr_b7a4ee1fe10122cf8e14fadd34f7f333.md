you will want to use IP addresses that are unique to your installation. You may want to change the settings of the notify statements.

**named.conf** The **named.conf** file in this example limits the IP addresses that **named** answers queries from and sets up logging (next page).

```
$ cat /etc/bind/named.conf
    options {
        directory "/etc/bind";
        // recursion NO;
        allow-query {127.0.0.1; 192.168.0.0/24};
    };
    zone "" IN {
        type hint;
        file "db.root";
    };
    zone "0.168.192.in-addr.arpa" IN {
        type master;
        file "named.conf.local";
        notify NO;
    };
    zone "sam.net" IN {
        type master;
        file "sam.net";
        notify NO;
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

The **allow-query** statement in the Options clause specifies the IP addresses of systems the server answers queries from. You must include the local system as 127.0.0.1 if it will be querying the server. The server is authoritative for the zone **sam.net**; the zone file for **sam.net** is /etc/bind/sam.net.