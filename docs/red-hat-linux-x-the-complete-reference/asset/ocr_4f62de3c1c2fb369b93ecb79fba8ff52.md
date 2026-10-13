preventing any zone transfers.

# named.conf Example

The following example is a simple named.conf file based on the example provided in the BIND documentation. This example shows samples of several of the configuration statements. The file begins with comments using C++ syntax, //. The options statement has a directory entry that sets the directory for the zone and cache files to /var/named. Here, you find your zone files, such as named.local and reverse mapping files, along with the cache file, named.ca. The first zone statement (.) defines a hint zone specifying the root name servers. The cache file listing these servers is named.ca. The second zone statement defines a zone for the mytrek.com domain. Its type is master, and its zone file is named "mytrek.com." The next zone is used for reverse IP mapping of the previous zone. Its name is made up of a reverse listing of the mytrek.com domain's IP address with the term IN-ADDR.ARPA appended. The domain address for mytrek.com is 192.168.0, so the reverse is 1.168.192. The IN-ADDR.ARPA domain is a special domain that supports gateway location and Internet address-to-host mapping. The last zone statement defines a reverse mapping zone for the loopback interface, the method used by the system to address itself and enable communication between local users on the system. The zone file used for this local zone is named.local.

# named.conf

```
//
// A simple BIND 9 configuration
//

logging {
    category cname { null; };
};

options {
    directory "/var/named";
};

zone "." {
    type hint;
    file "named.ca";
};

zone "mytrek.com" {
    type master;
    file "mytrek.com";
};

zone "1.168.192.IN-ADDR.ARPA" {
    type master;
    file "192.168.0";
};

zone "0.0.127.IN-ADDR.ARPA" {
    type master;
```