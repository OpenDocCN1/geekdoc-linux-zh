# 728 Linux Administration: A Beginner's Guide

dynamic-boot-lease-cutoff BOOT clients are not aware of the lease concept. By default, the DHCP server assigns an IP address that never expires. In certain situations, it may be useful to have the server stop issuing addresses for a set of BOOT clients. In these cases, this parameter is used. This parameter's syntax is as follows:

```
dynamic-boot-lease-cutoff date;
```

The date is specified in the form W YYYY/MM/DD HH:MM:SS, where W is the day in cron (0–Sunday,6–Saturday), YYYY is the year, MM is the month (01=January,12=December), DD is the two-digit format, HH is the two-digit hour in 24-hour format (0=Midnight,23=p.M.), MM is the two-digit representation of minutes, and SS is seconds.

dynamic-boot-lease-length Although the BOOT clients don't have a mechanism for expiring the addresses they receive, it's sometimes to save the server assume that they aren't using the address anymore, freeing it for further use. This is useful if the BOOT application is known to be short in duration. If so, the server can set the number of seconds and expire it after that time has passed.

```
dynamic-boot-lease-length seconds;
```

> CAUTION Use the dynamic-boot-lease-length parameter with caution, as it can introduce problems if it issues an address before another host has stopped using it.

filename In some applications/environments, the DHCP client may need to know the name of a file to use boot. This is often combined with next-server to retrieve a remote file for installation configuration or diskless booting. This parameter's syntax is as follows:

```
filename filename;
```

fixed-address or fixed-address6 This parameter is only applicable under the host declaration. It specifies the set of addresses (IPv4 or IPv6) assignable to the client. This parameter's syntax is as follows:

```
fixed-address address [, address];
fixed-address ip6-address [, ip6-address];
```

get-lease-hostnames If this parameter is set to true, the server will resolve all addresses in the declaration space and use that for the hostname option. This parameter's syntax is as follows:

```
get-lease-hostnames [true | false];
```