```
  };
zone "0.0.127.in-addr.arpa" {
  type master;
  file "named.local";
};
```

The only other file needed is a *hint* file, which normally comes with a distribution of BIND.

**Exam Tip** A caching-only name server increases performance for clients by caching the answers to queries for later use. They are easy to set up since they are not responsible for any zone information.

# ## Using BIND v4

**Exam Tip** BIND v4 uses the *named.boot* configuration file.

The earlier version of BIND was v4. The old v4 is not widely used today, and the only work being done on it is security fixes, when they arise. It is not recommended to use v4 in most cases. The LPI exam requires you to know the differences between v4 and v8, but not how to configure v4. Unlike v8, v4 does not use a *named.conf* file but instead uses a *named.boot* file. The following is an example of a *named.boot* file:

```
; tell what subdir has the lookup database files
directory    /namedb
; type      domain                source host/file
backup file
cache
root.cache
primary   0.0.127.IN-ADDR.ARPA   localhost.rev
; example primary server config:
primary  mydomain.com mydomain
primary  1.168.192.IN-ADDR.ARPA mydomain.rev
```

The zone files are very similar to those in v8. Table 16-32 lists the configuration entries in *named.boot*.