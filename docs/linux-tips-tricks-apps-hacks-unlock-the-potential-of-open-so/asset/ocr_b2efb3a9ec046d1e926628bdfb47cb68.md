# 01 Install BIND

BIND stands for Berkeley Internet Name Domain and is an implementation of the DNS protocols. On a Debian 7 system you can install the latest version of BIND by running the following command:

```
`# apt-get install bind9`
```

To find your version of BIND, execute the following command:

```
`# named -v`
`BIND 9.8.4-rpz2+1005:12-P1`
```

![](bbox=[0.11, 0.68, 0.33, 0.81])

# 02 What is Cache DNS server?

A caching-only DNS server does not contain information about a domain; it just contains information based on the results of the DNS queries it has already performed. The main reason that DNS caching works well is because DNS data does not change frequently.

![](bbox=[0.11, 0.18, 0.62, 0.49])

# 03 The host utility

Host produces a clean output and that is the main reason for liking it – it can easily be used inside shell scripts. Its last parameter, which is optional, is the name of the DNS server to ask. If not given, it uses the /etc/resolv.conf file to find a DNS server.

Used with the -mx parameters, host shows the mail servers for a domain or subdomain:

```
`# host -mx linuxuser.co.uk`

linuxuser.co.uk.mail is handled by 10
mail.imagene-publishing.co.uk.
linuxuser.co.uk.mail is handled by 20
mail2.imagene-publishing.co.uk.
```

The numbers that you see after the “handled by” are the preference values that indicate the mail exchanger’s priority. A preference value by itself is not important. What is important is its relationship to the other values.

Mail servers should attempt to deliver to the mail exchangers with the lowest values first. If the delivery fails for some reason, then the mail exchanger with the next highest value will be tried. If two or more mail exchangers have the same preference value, it is up to the mail server to decide which one to choose. The primary DNS server is responsible for defining the email server for a domain or subdomain.

Used with the -t ns parameters, host shows the DNS Servers for a domain.

# 04 The dig utility

The dig utility can show you the same DNS related information as host, however, dig’s output is more populated by default. In order to find the DNS servers of the .co.uk domain with the help of dig, you could do this by executing the following command:

```
`$ dig co.uk ns`

Trying to perform a AXFR query with dig fails:
`$ dig @localhost co.uk axfr`
```

```
`<<> DiG 9.8.4-rpz2+1005:12-P1 <<> @`
`localhost co.uk axfr`
`(2 servers found)`
`; global options: +cmd`
`; Transfer failed.`
```

AXFR is a mechanism for replicating DNS data across DNS servers, but it can also be used for evil purposes. The DNS Administrator is responsible for allowing the access to the AXFR protocol to specific machines and restricting it to the rest of the world.

# 05 The /etc/resolv.conf file

The quickest way to see your DNS configuration is by looking at the /etc/resolv.conf file, where you can see the IP address for each DNS server used; each entry starts with the nameserver keyword. There is no point in using anything but an IP address for a DNS server. Usually, the administrator deals with this file when setting up a Linux machine; otherwise it is populated when your Linux machine gets its network configuration using DHCP.