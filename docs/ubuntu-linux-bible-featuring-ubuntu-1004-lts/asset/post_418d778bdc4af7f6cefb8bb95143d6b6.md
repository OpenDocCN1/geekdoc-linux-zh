
# Tip

As always with server packages such as BIND, I suggest that you install BIND using aptitude from the command line. This will enable you to use the -r option to automatically install the packages that are recommended for use with BIND. They don't use disk space, and having more tools is always better! ■

After installing the bind9 package, setting up your own DNS server is a simple matter of creating a few configuration files, as explained in the next section.

# Overview of BIND Configuration Files

The /etc/nsswitch.conf and /etc/resolv.conf files reflect your general approach to resolving hostname and IP addresses. The primary configuration file for the BIND server, named.conf, is found in the directory /etc/bind on Ubuntu systems.

As delivered by Ubuntu systems, the /etc/bind/named.conf file primarily consists of states that load BIND configuration files, providing a simple, hierarchical structure for your BIND configuration files. The files that an Ubuntu BIND server loads fall into several categories:

- Configuration files for the BIND server process, named.. BIND installations load a general, site-independent configuration file and a separate, site-specific configuration file. This simplifies updates making it easier to identify files that may have changed in the BIND installation on a specific system.
- Zone files that define the mapping of hostnames in DNS zone to IP addresses
- Reverse lookup files that define the mapping of IP addresses in a numeric DNS zone to hostnames

As a specific example, the default /etc/bind/named.conf file loads the following files. These are listed in alphabetical order to simplify finding a file in this list rather than in the order that they are actually loaded:

- /etc/bind/db.0: Contains reverse lookup information that resolves the broadcast addresses 0.*
- /etc/bind/db.127: Contains reverse lookup information that resolves the loopback addresses 127.*
- /etc/bind/db.255: Contains reverse lookup information that resolves the loopback addresses 255.*
- /etc/bind/db.empty: Contains a shared file that is used for each of the non-routable IP address families specified by RFC 1918, "Address Allocation for Private Internets" (www.rfc.org/rfccs/rfc1918.html).
- /etc/bind/db.local: Contains hostname to IP address information for the local loopback interface, 127.0.0.1.

# Chapter 3: Setting Up a DNS Server

- /etc/bind/db.root: Contains hostname to IP address information for the root name servers.
- /etc/bind/named.conf.local: Contains zone entries that identify any zones and IP addresses for this BIND server is a source of authoritative information. This is a local, host-specific supplement to the file /etc/named.conf.
- /etc/bind/named.conf.options: Defines the basic options with which the local BIND server has been configured.
- /etc/bind/zones.rfc1918: Provides reverse lookup information for each of the non-routable IP families specified by RFC 1918, "Address Allocation for Private Internets" (http://www.faqs.org/rfc/rfc1918.html). This file is not loaded by Ubuntu BIND server by default, but can be loaded in your /etc/bind/named.conf.local file to reduce the time spent trying to resolve IP addresses in non-routable networks.

In most cases, you will only modify the /etc/bind/named.conf.local file for your BIND server. In this file, you will add entries for files that define the zones and IP address ranges for which your BIND server can provide authoritative DNS information.

The /etc/bind/named.conf.options file configures BIND servers running on Ubuntu systems those servers to use /var/cache/bind as their default working directory. For this reason, all temporary DNS data is stored in that directory. All paths in the /etc/bind/named.conf.local file should either be the full pathnames of files located in non-transient directories in your filesystem, such as /etc/bind/, or will be interpreted as files that are to be found in /var/cache/bin. ■

A sample /etc/bind/named.conf.local file from one of my DNS servers looks like the following:

```
zone "vonhagen.org" {
  type master;
  file "/etc/bind/vonhagen.zone";
  check-names warn;
}

zone "168.192.in-addr.arpa" {
  type master;
  file "/etc/bind/168.192.in-addr.arpa";
}

include "/etc/bind/zones.rfc1918.local";
```

As you can see, this DNS server is a master server for the zone vonhagen.org, which uses IP addresses in the 192.168.*. Information about the zone vonhagen.org is provided in the file /etc/bind/vonhagen.zone. Reverse lookup information for IP addresses in the 192.168.* family is provided in the file /etc/bind/168.192.in-addr.arpa. As discussed previously, full pathnames must be provided for any files not found in /var/cache/bind, and which is the default BIND server's default directory. This file also loads a local copy of the default /etc/bind/zones.rfc1918 file, which I have edited to remove null responses for the zone "168.192.in-addr.arpa" that I use locally.

The next section explains how to create the zone and reverse lookup files for any local systems for which your BIND server will provide authoritative information.

# Creating DNS Zone and Reverse Lookup Files

As installed on Ubuntu systems, BIND is a caching-only name server that is appropriate for use on local servers or heavily network-dependent systems to help minimize the amount of external DNS traffic by caching DNS lookups so subsequent requests for that information can be provided from the cache rather than repeating an external DNS request.

Many people want to run their own DNS servers provide DNS information for the hosts that they are responsible for on their home, enterprise, or academic networks. As discussed earlier in this chapter, DNS information for each set of hosts and associated range of IP addresses specified in a zone file, one identifies the IP address associated with a specific hostname (known as IP address lookups), and one for reverse lookups that identify the hostname.

# Note

One confusing about the SOA record (and, frankly, about many other file entries) is that many of the files have default values and are therefore omitted if the values you specify are the same as the defaults. Personally, I find the practice of omitting values to be both lazy and the most common DNS problems. The parser for DNS files is quite finicky (to use the technical term), you will eventually bury yourself or one of your fellow sysadmins by leaving fields out. It is not as if any of the values in an SOA or other records in a zone or reverse lookup file are all long or require that much typing. Do everybody a favor—specify all them.

## Using Common Entries for Zone and Reverse Lookup Files: SOA and $TTL

The most important entry in a zone or lookup file is the Start of Authority (SOA) record, which defines the global parameters for the zone. The format of an SOA record is defined in RFC 1035 (www.rfc.org/rfc/rfc1035.html). A sample SOA record looks like the following:

```
@1d IN SOA vonhagen.org. vonhagen.org. (
  200809102 : Serial
  21600 : Refresh
  1800 : Retry
  604800 : Expiration
  900 : Negative Cache TTL)
```

# Tip

One confusing about the SOA record (and, frankly, about many other entries) is that many of the files have default values and are therefore omitted if the values you specify are the same as the defaults. Personally, I find the practice of omitting values to be both lazy and the most common DNS problems.

The fields in an SOA record are:

1. The first field identifies the root name of the zone associated with this SOA record. The @symbol is a shortcut for this name, which is specified in the declaration of the BIND configuration file (in this case, the file /etc/bind/named.conf.local).
2. The second field is the TTL to this record. Even though I always put a default value at the beginning of a zone file, I simply repeat that value to be more precise. This field is technically optional—if it is not specified, the default TTL for the server or an internal default will be used.
3. The third field identifies the record class of the SOA record. An IN entry identifies this as a DNS resource of the Internet class. This field is technically optional because IN is the default class type for any resource record in a zone or reverse lookup file, but I prefer to explicitly provide a class value for readability and clarity. Other possible record classes are HS (Hesiod) and CH (Chaos), which are types of records that only MIT staff or Lisp machine fans will recognize.
