
# The Internet Systems Consortium, isc.org 623

As the internal view, nicknames are implemented with A records. Very few hosts are actually visible in the external world view, although that's not immediately apparent from these truncated excerpts. Note that machines that appear in both views (for example, ns1.atrust.com) have RFC1918 private addresses internationally but really real addresses.

The TTL in these zone files is set to 16 hours (57,600 seconds). For internal zones, the TTL is one day (86,400 seconds). Most individual records in zone files are not assigned an explicit TTL value.

The bizarre PTR records at the end of the external file allow atrust.com's ISP to delegate the reverse mapping of a very small piece of address space. CNAME records at the ISP's site enable this variation of the CNAME hack to work; save 585 for more information.

# The Internet Systems Consortium, isc.org

ISC is the author and maintainer of BIND as well as the operator of the Root name server. ISC also runs a TLS server that serves many top-level domains. That's why we call them experts!

Below are snippets from their configuration files. Notice that they are using both IPv4 and IPv6. They also use TSIG encryption to authenticate between master and slave servers for zone transfers. The transfer-source options ensure that the source IP addresses for outgoing zone transfer requests confirm to the specifications allow-transfers statements on the master servers.

# The named.conf file:

```
// isc.org TLD name server

options {
    directory "var/named";
    datasize 1000M;
    listen-on { 204.152.184.64 };
    listen-on-v6 { 2001:4f8:0:2::13 };
    recursion no;
    transfer-source 204.152.184.64;
    transfer-source-v6 2001:4f8:0:2::13;
}

// rndc_key
key rndc_key {
    algorithm hmac-md5;
    secret "<secret>";
}

// TSIG key for name server ns-ext
key ns-ext {
    algorithm hmac-md5;
    secret "<secret>";
}
```

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
include "in/named.zones";
include "master.zones";
include "slave.zones";
// Root, localhost, 127.0.0.1, ::1
// Zones we master
// Lots of slaves
```

These include keep the named.conf file short and tidy. If you serve lots of zones, consider breaking up your configuration into bite-sized pieces like this. importantly, set up your filesystem hierarchy so that you have a directory with a thousand zone files in it. Modern filesystems handle large-directories efficiently, but they can be a management hassle.

Here’s more from the file master.zones:

```
zone "isc.org" {
  type master;
  file "master/isc.org";
  allow-update { none };
  allow-transfer { none };
}
```

```
zone "sfo2.isc.org" {
  type master;
  file "master/sfo2.isc.org";
  allow-update { none };
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
  file "secondary/vix.com";
  masters { 204.152.188.234 };
}
```

```
zone "cix.net" {
  type slave;
  file "secondary/cix.net";
  masters { 204.152.188.234 };
}
```

The allow-transfer clause set to none in the master.zones files implies that ISC is using multiple master servers—someone has to implement zone transfers to the slave servers.

# 17.11 The NSD/UNBOUND SOFTWARE

With BIND configuration out of the way, we now introduce an alternative DNS server implementation that offers some nice features along with speedy performance. NSD, the Name Server Daemon, was developed by NLNet in 2003. The original intention of the project was to develop an alternative implementation independent of BIND that could be used on root servers, making the root zone more robust through software diversity. Three root servers and top-level domains now use NSD, but you don't have to be a root server or TLD to benefit from NSD's robustness, speed, and simplicity.

Two programs form the core of the NSD software: zonec, a zone file compiler that converts text-format DNS files into databases; and nsd, the name server daemon itself. NSD precomputes and indexes all possible answers to the valid queries it may receive, unlike BIND, which creates its answers on the fly, NSD has the answers in an outgoing packet in a single memory copy, making it incredibly fast.

Unbound is a recursive DNS server that is complementary to NSD. Developed in C by NLNet from a Java implementation by Verisign, Memory, Kire, and EP.NET. NSD and Unbound provide flexible, fast, secure DNS service appropriate for most sites. The NLNet components are not as mature as BIND and do not have many bells and whistles, but they are free for most sites.

ldns, a library of routines that make it easier to write DNS software tools, is also available for use with the NSD and Unbound distributions. It includes a directory of examples: several tools aimed primarily at DNSSEC, a DNSSEC signer tool, and drill, a debugging tool similar to BIND's dig. You can download all them from nlnet.nl. NLNet has also built a tool called Autrust that does RFC5011 rollover and key management. It is being integrated into Unbound; we do not cover it here.

The DNSSEC code in NSD/Unbound is more robust and better than in BIND. It is also faster. For example, Unbound is five times faster than BIND at verifying DNSSEC signatures. BIND still has an edge in some areas, notably in documentation and in extra features. For a truly robust DNS regime, run both!

# Installing and configuring NSD

First, create a user nsd on the system where name server will run. Then log in as nsd, download the NSD/Unbound packages (currently three of them: NSD, Unbound, and ldns), and unpack. To install nsd, follow the directions in doc/README file, basically:

```
$ configure
sudo make
sudo make install
```

# Fundamental differences from BIND

The Table 17.10 shows where NSD installs or expects things to be default.

# Table 17.10 NSD installation directories

| Item | Directory |
| --- | --- |
| Binaries | /usr/local/sbin |
| Sample config file | /etc/nsd |
| Man pages | /usr/local/share |
| Text zone files | /etc/nsd |
| Compiled zone files | /var/db/nsd |
| PID file | /var/run |

It seems a bit rude for NSD to put the zones beneath /etc, or somewhere in usr/local or /var. Considering the files are large. You can use configure to change things if you don't like NSD's choices; the makefile is quite readable. The output of configure goes to the file config.log in the install directory, so you can sort through it if there is a problem.

The NSD installs seven programs:

- **nsd** – the name server daemon
- **nsdc** - a script that controls NSD by sending signals
- **zonec** - converts zone files to database files
- **nsd-notify** – sends notification messages (deprecated)
- **nsd-xfer** - receives zone files (deprecated)
- **nsd-checkconf** - checks the syntax of nsd.conf
- **nsd-patch** - reflects database updates to zone files

If you are used to BIND, a few things in NSD will seem strange at first. For example, there no root hints file and no need to include localhost zones. NSD also has no support for views, if your site publishes different versions of the DNS data inside and outside your organization, you will have to stick to BIND or use multiple instances of nsd. Dynamic updates are also unsupported. Since NSD is an authoritative-only server, many of BIND's bells and whistles do not operate.

BIND reads zone files and keeps them in memory; NSD compiles zone files into a database format and uses both memory and disk for the database.

**nsd's** configuration language is simpler than BIND's. There are no semicolons to forget, no braces to group things, and only three top-level statements: *server, zone, and key*. Comments are introduced with the # sign. Options under each of the three statements have the form

```
attribute: value
```
