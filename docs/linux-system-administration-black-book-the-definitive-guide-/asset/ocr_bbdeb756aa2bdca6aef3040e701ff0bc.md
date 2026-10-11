5. Unless you have a specific reason not to, it is a good idea to set up caching for the master name server, because this speeds up name-lookup times. Here’s an example of a filled-in caching server statement:

```
```
zone "." {
    type hint;
    file "Master.cache";
};
```
```

> **NOTE:** *This file is stored in /etc/named, because that is what I set as the directory in Step 4.*

6. Create your reverse local zone. As described in the In Depth section “Introduction To /etc/named.conf”, this zone’s address is in reverse IP format. The reverse local zone statement for the network 192.168.90.0 might be as follows:

```
```
zone "0.0.127.in-addr.arpa" {
    type master;
    file "reverse.local";
};
```
```

> **NOTE:** *Your reverse local zone will always have this name, regardless of your network address.*

7. Create your domain zone. For the domain animals.org, you might use the following:

```
```
zone "animals.org" {
    type master;
    file "animals.org";
    notify yes;
};
```
```

> **NOTE:** *When used in a zone, options do not have to be braced within an options statement.*

8. Create the reverse domain zone. This zone covers the entire network, so no host numbers are needed. Using the data already given in this example, the reverse domain zone might be as follows:

```
```
zone "90.168.192.in-addr.arpa" {
    type master;
    file "90.168.192";
    notify yes;
};
```
```