In the named.conf file, the IP6.ARPA localhost entry would look like this.

```
zone "\[x00000000000000000000000000000001/64].IP6.ARPA" in {
    type master;
    file "192.168.0.";
};
```

In the localhost reverse mapping file, the localhost entry would appear like this.

```
\[x0000000000000001/64]    IN    PTR    localhost.
```

For the older IP6.INT format, the localhost entry would use the same network address of zeros, but the localhost reverse mapping file would use a nibble format for the address, as shown here.

```
1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0    IN    PTR    localhost.
```

# Subdomains and Slaves

Adding a subdomain to a DNS server is a simple matter of creating an additional master entry in the named.conf file, and then placing name server and authority entries for that subdomain in your primary DNS server’s zone file. The subdomain, in turn, has its own zone file with its SOA record and entries listing hosts, which are part of its subdomain, including any of its own mail and news servers.

# Subdomain Zones

The name for the subdomain could be a different name altogether or a name with the same suffix as the primary domain. In the following example, the subdomain is called beach.mytrek.com. It could just as easily be called mybeach.com. The name server to that domain is on the host crab.beach.mytrek.com, in this example. Its IP address is 192.168.0.33 and its zone file is beach.mytrek.com. The beach.mytrek.com zone file holds DNS entries for all the hosts being serviced by this name server. The following example shows zone entries for its named.conf:

```
zone "beach.mytrek.com" {
    type master;
    file "beach.mytrek.com";
};

zone "1.168.192.IN-ADDR.ARPA" {
    type master;
    file "192.168.0.";
};
```

# Subdomain Records

On the primary DNS server, in the example turtle.mytrek.com, you would place entries in the master zone file to identify the subdomain server’s host and designate it as a name server.