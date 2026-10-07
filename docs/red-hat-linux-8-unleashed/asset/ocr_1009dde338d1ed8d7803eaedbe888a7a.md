# CHAPTER 14 Managing DNS

```
May 23:48:33 shuttle named named[2608]: loading configuration from '/etc/named.conf'
May 23:48:33 shuttle named named[2608]: no IPv6 interfaces found
May 23:48:33 shuttle named named[2608]: listening on IPv4 interface lo, 127.0.0.1#53
May 23:48:33 shuttle named named[2608]: named startup succeeded
May 23:48:33 shuttle named named[2608]: listening on IPv4 interface\
eth0, 192.168.2.68#53
May 23:48:33 shuttle named named[2608]: command channel listening on 127.0.0.1#953
May 23:48:33 shuttle named named[2608]: zone 0.0.127.in-addr.arpa/IN:
loaded serial 199702200
May 23:48:33 shuttle named named[2608]: zone localhost/in: loaded serial 42
May 23:48:33 shuttle named named[2608]: running
```

You can use rndc to connect to this instance of named. Running rndc without arguments displays a list of available commands, including the ability to reload or refresh zones, dump statistics and the database to the disk, toggle query logging, and stop the server.
(Unfortunately, rndc does not implement all the commands that were supported by older versions of BIND.)
dc—the control program shipped with earlier versions of BIND.

You should be able to resolve 1.0.0.127.in-addr.arpa locally (try dig @localhost) and other names via recursive resolution. If you cannot, something is wrong, and you should read the "Troubleshooting" section later to diagnose and correct your problem before proceeding further. Remember to read the logs!

# Providing DNS for a Real Domain

You can expand the minimal nameserver configuration you created into one that performs useful name service for a real domain. Suppose that your ISP has assigned to you the IP addresses in the 192.2.0/29 range which has six addresses: 192.2.0.1-6 and that you want to serve authoritative data for the domain example.com. A friend has agreed to configure her name server (192.2.0.96) to be a slave for the domain, as well as a backup mail server. In return, she wants the foo.example.com subdomain delegated to her own servers.

# Forward Zone

First, we must introduce the zone to named.conf

```
| zone "example.com" {
|   type master;
|   file "example.com";
| };
```