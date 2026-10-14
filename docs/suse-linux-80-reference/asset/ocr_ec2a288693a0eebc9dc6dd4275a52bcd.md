```
```conf
options {
    directory "/var/lib/named";
    forwarders 10.0.0.1;
    notify no;
};

zone "localhost" in {
    type master;
    file "localhost.zone";
};

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "127.0.0.zone";
};

zone "." in {
    type hint;
    file "root.hint";
};
```
```

*File 46: A Basic /etc/named.conf*

This example works for both BIND8 and BIND9, because no special options are used that are only understood by one version or the other. BIND9.1.1 accepts all BIND8 configurations and makes note of options not implemented at start-up. Special BIND9 options are, however, not supported by BIND8.

# Important Configuration Options

**directory "/var/lib/named";** specifies the directory where BIND can find the files containing the zone data.

**forwarders 10.0.0.1;** is used to specify the name servers (mostly the provider) to which DNS requests, which cannot be resolved directly, are forwarded.

**forward first;** causes DNS requests to be forwarded first before an attempt is made to resolve them via the root name servers. Instead of forward first, forward only can be written to have all requests forwarded and none sent to the root name servers. This makes sense for firewall configurations.