Long-time users of `nslookup` may be surprised to see their old friend being put away. Well, the news isn’t as bad as you think—the BIND team is simply trying to leave less overlap between its tools.

In its simplest use, `host` allows you to resolve host names into IP addresses from the command line. For example:

```
[root@tux root]# **host theorb.com**
thorb.com has address 209.133.83.16
```

We can also use `host` to perform reverse lookups. For example:

```
[root@tux root]# **host 209.133.83.16**
16.83.133.209.IN-ADDR.ARPA domain name pointer taz.hyperreal.org
```

This can lead to all kinds of interesting discoveries. In this case, we see that `thorb.com` is the same as `taz.hyperreal.org`. It is likely that `taz.hyperreal.org` is also “virtually hosting” other domains, as well.

![](bbox=[0.15, 0.47, 0.2, 0.52])

If you are familiar with `nslookup`, don’t worry, it’s still there. However, since the BIND group is trying to move people away from it, consider using the `dig` tool (discussed next) instead when you need to find out about records other than A and PTR, or when you need to query servers other than your own.

# dig

The domain information gopher, `dig`, is a great tool for gathering information about DNS servers. The typical format of the `dig` command is

```
[root@tux /root]# **dig @server domain query-type**
```

where `@server` is the name of the DNS server you want to query, `domain` is the domain name you are interested in querying, and `query-type` is the name of the record you are trying to get (A, MX, NS, SOA, HINFO, TXT, or ANY).

For example, to get the `mx` record for the domain `whitehouse.gov` from the DNS server `ns1.ucsd.edu`, you would run:

```
[root@ford /root]# **dig @ns1.ucsd.edu whitehouse.gov mx**
```

The program `dig` is incredibly powerful. You should read the man page that was installed with `dig` to learn how to use some of its more advanced features.