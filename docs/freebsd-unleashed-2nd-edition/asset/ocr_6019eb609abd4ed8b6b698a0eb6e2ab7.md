![](bbox=[0.23, 0.08, 0.75, 0.35])

FIGURE 31.2 A Diagram of a DNS lookup involving a forwarder providing cached DNS information in a nonauthoritative capacity to the local DNS and the client.

You can specify as many forwarders as you like, and `named` will consult each one before giving up and querying the root servers. You can additionally uncomment the `forward only;` statement in the `options` block to force `named` to consult only the forwarders on all queries. Normally, your machine will consult the forwarders for DNS data unless it appears that the forwarders are unreachable or broken, in which case it makes full queries to the root servers. Setting the `forward only;` option prevents it from making root server queries on any occasion.

# Master and Slave Configurations

Each zone block defines a domain or subdomain that your FreeBSD machine will administer. Most commonly, a zone block defines a domain of the form `somewhere.com:`

```
```
zone "somewhere.com" {
 type master;
 file "somewhere.com";
};
```
```

All that’s absolutely necessary in this block is the name of the domain or subdomain (without the trailing dot that will usually be associated with a zone name), the `type` statement that defines whether it’s a master or slave configuration for that domain, and the name of the file that contains the zone information. Let’s examine what it means for a name server to act as a master or a slave for a particular zone.

The `type` substatement can be `master`, `slave`, `stub`, `forward`, or `hint`. The most commonly used of these are `master` and `slave`; the rest are used in special circumstances only, which we will look at shortly.