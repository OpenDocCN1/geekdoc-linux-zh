Unfortunately, rndc does not yet implement all the commands that were supported by ndc—the control program shipped with earlier versions of BIND.

You should now be able to resolve 1.0.0.127.in-addr.arpa locally (try dig @localhost 1.0.0.127.in-addr.arpa PTR +norec) and other names via recursive resolution. If you cannot accomplish this resolution, something is wrong, and you should read the "Troubleshooting DNS" section later in this chapter to diagnose and correct your problem before proceeding further. Remember to read the logs!

# Providing DNS for a Real Domain

You can expand the minimal nameserver configuration you just created into one that performs useful name service for a real domain. Suppose that your ISP has assigned to you the IP addresses in the 192.0.2.0/29 range (which has six usable addresses: 192.0.2.1–6) and that you want to serve authoritative data for the domain example.com. A friend has agreed to configure her nameserver (192.0.2.96) to be a slave for the domain, as well as a backup mail server. In return, she wants the foo.example.com subdomain delegated to her own nameservers.

# Forward Zone

First, we must introduce the zone to named.conf:

```
zone "example.com" {
type master;
file "example.com";
};
```

and create the zone file:

```
$TTL 20

@ SOA ns1.example.com. hostmaster.example.com. (
2001090101 ; Serial
24h ; Refresh
2h ; Retry
3600000 ; Expire (1000h)
1h) ; Minimum TTL
NS ns1.example.com.
NS ns2.example.com.
MX 5 mx1.example.com.
MX 10 mx2.example.com.
A 192.0.2.1
```