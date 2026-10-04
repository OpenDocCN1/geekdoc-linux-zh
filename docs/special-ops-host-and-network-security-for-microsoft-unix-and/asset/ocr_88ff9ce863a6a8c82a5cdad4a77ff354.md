# Chapter 8 · Attacking and Defending DNS

```
ns.example.com.      ; mname/origin
admin.example.com.      ; rname/contact
```

The @ symbol will return the domain name. In the following example, all @ symbols will be returned at example.com.

A domain-specific administrative e-mail contact should be used on every domain name. The syntax of the e-mail cannot contain a @; therefore a period is used as a standard:

```
2001102401              ; serial
1d                      ; refresh
1h                      ; retry
1w                      ; expire
1d )                   ; minimum

IN NS                    ns1.example.com.
IN  MX                    10 @
IN  A                     127.0.0.1
```

A blank record like the one will be used when a subdomain is unused; for instance, that record will be used for queries on example.com:

```
* IN  A                     127.0.0.1
```

The * is a wildcard; the preceding line will be returned for any query. For example, all.work.and.no.play.makes.johnny.a.dll.boy.example.com, www.example.com, fbp.example.com, and dns.can.be.fun.example.com will all receive this query response as designated by the wildcard.Remember that records in a zone file are read from top to bottom, wildcard entries will be at the bottom of zone files.

After your server is running, make sure you have a firm understanding of the daemon. When you are ready, custom modifications should be made to secure the server.

To hide the BIND version, create a.db file, include the following TXT records, and replace the text as it fits your needs:

```
$TTL  1D
$ORIGIN bind.
@    1D      CHAOS  SOA      localhost.root.localhost. (
                   2001013101      ; serial
                   3H              ; refresh
                   1H              ; retry
```

![](bbox=[0.068, 0.943, 0.292, 0.966])