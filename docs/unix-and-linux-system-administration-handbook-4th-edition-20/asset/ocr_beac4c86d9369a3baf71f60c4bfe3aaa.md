# Chapter 17 DNS: The Domain Name System

```
server 204.152.188.234 { keys { ns-ext }; };
```

```
controls {
  inet 204.152.188.64 allow { any }; keys { rndc_key };
}
```

```
include "inff/named.zones";ninclude "master.zones";ninclude "slave.zones";
// Root, localhost, 127.0.0.1, ::1
// Zones we master
// Lots of slaves
```

These include keep the named.conf file short and tidy. If you serve lots of zones, consider breaking up your configuration into bite-sized pieces like this. importantly, set up your filesystem hierarchy so that you have a directory with a thousand zone files in it. Modern filesystems handle large-directories efficiently, but they can be a management hassle.

Here’s more from the file master.zones:

```
zone "isc.org" {
  type master;
  file "master/isc.org";n  allow-update { none };
  allow-transfer { none };
}
```

```
zone "sfo2.isc.org" {
  type master;
  file "master/sfo2.isc.org";n  allow-update { none };
  allow-transfer { none };
}
```

```
// Lots of zones truncated
```

And from slaves.zones:

```
zone "vix.com" {
  type slave;
  file "secondary/vix.com";n  masters { 204.152.188.234 };
}
```

```
zone "cix.net" {
  type slave;
  file "secondary/cix.net";n  masters { 204.152.188.234 };
}
```

The allow-transfer clause set to none in the master.zones files implies that ISC is using multiple master servers—someone has to implement zone transfers to the slave servers.