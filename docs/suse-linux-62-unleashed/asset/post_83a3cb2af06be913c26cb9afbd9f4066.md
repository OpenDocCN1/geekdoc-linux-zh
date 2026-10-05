
# Networking and Internet Services
PART II

By default, BIND 8 has the DNS boot file /etc/named.conf. Version 4 implementations default to the boot file /etc/named.boot. SuSE 6.2 no longer ships with an /etc/named.boot file.

BIND 8 has host naming, which might break with naming conventions accepted by older BIND versions. Rather than letting this deter you from using the superior BIND 8, you can temporarily turn off host naming check with the following three lines in the options section of named.conf:

```
check-names master ignore;
check-names slave ignore;
check-names response ignore;
```

Because BIND 8 comes with SuSE Linux 6.2, and because it's easier and more secure, BIND 8 is covered exclusively in this chapter.

# A Word About This Chapter's Examples

The examples in this chapter were created to illustrate specific points, and to allow the reader to safely run them on a two-computer network. To accomplish this with minimal risk to the worldwide DNS system or your company's DNS system, all examples use the imaginary top domain name .cxm.

In addition, all examples use private IP subnet 192.168.42.0/24. This is one of the subnets set aside for local, non-Internet use. You can see the complete list of private IP subnets in document RFC 1918, mirrored at http://www.isi.edu/in-notes/rfc1918.txt. If your company already uses the 192.168.42 numbers for in-house IP addresses, pick another private subnet for this chapter's examples.

If running this chapter's examples happens to release any information to a higher level or the worldwide DNS top-level domain and the private IP numbers would instantly be as garbage to ignore.

DNS is complex, and one of the systems on your network that depends intimately on the correct working of machines elsewhere.

Likewise, machines elsewhere depend intimately on the correct working of your DNS system. In the world of real top-level domains and public IP addresses, an unnoticed error in your DNS setup can cause serious problems thousands of people miles away, which turn can cause serious problems for you.

When doing real-world DNS, please keep the following rules in mind:

# The Domain Name Service
CHAPTER 8

- Do not set up DNS for a zone until you have received delegation of authority that zone.
- Always make sure your reverse and forward zones agree with each other.
- Always maintain at least one secondary DNS server over a zone to avoid having a single point of failure. Ideally, the secondary DNS server should be on a separate subnet, preferably through a separate ISP.
- Check and recheck your setup for errors. Make sure, for example, that you restart named, that it is actually running. Otherwise, you have no name service.

To best illustrate specific points, this chapter's examples do not consistently follow all these rules. We suggest that if you want to run this chapter's examples, do so on a pair of machines not presently serving DNS for your organization, and make sure to use the bogus .cxm top-level domain and the private 192.168.42 subnet.

# Bringing Up a Trivial Caching DNS

A normal SuSE 6.2 installation includes an almost-working caching DNS implementation.

This section discusses the fundamentals of a caching DNS and introduces some terminology and concepts.

For the purposes of this exercise, assume brand new machine numark, domain domain.cxm, assigned IP address 192.168.42.1 with primary DNS set to that same IP.

> Caution

Before editing any configuration file, back it up. Original distribution or installation-default files should be backed up. The best method of doing this is use rcs (Revision Control System) as follows:

```
ci /etc/named.conf
co -l /etc/named.conf
```

This creates a history file called /etc/named.conf,v with a revision history. It also allows you to write to the normal named.conf. After each set of changes, use the ci command to check in the new changes. With rcs, you can keep a long history of changes and revert incorrect changes easily.

# Networking and Internet Services
PART II

# Note

This chapter will use hypothetical top-level domain .cxm (note the x) to prevent any chance of causing confusion on the Internet. For the same reason, we use IP addresses in the Private Address Space defined in RFC 1918, mirrored at http://www.isi.edu/in-notes/rfc1918.txt. These names and addresses will work for the examples in this book.

Of course, if you're doing a genuine Internet-connected DNS, put in the domain name and IP address assigned to your organization by proper authorities.

Listing 8.1 contains the installation default /etc/resol.conf file for new host.

# LISTING 8.1 The /etc/resol.conf file

```
search domain.cxm
nameserver 192.168.42.1
```

The resolv.conf file configures the DNS client, not the DNS server, even though in many cases they coexist on the same computer. The first line of resolv.conf defines domain.cxm as the client's default domain. The domain that's appended to machine names. The second line defines the IP address of the DNS server used by the client. SuSE 6.2 contains a lengthy /etc/named.conf file used to demonstrate the use of various parameters. In this file, anything preceded by // or enclosed in /** is a comment. In English, the named.conf file says the following:

* All zone data files mentioned in named.conf shall be relative to directory var/named/.
* The root of the zone tree, hints to which are given in named.conf, which is a list of the root servers.
* Any IP address in subnet 127.0.0 shall be resolved according to zone data file 127.0.zone, which is used, but not created by the DNS server. Had it been type slave instead of type master, the file would have been created by zone transfer from a master zone on another computer. When you're working with named.conf, remember that syntax is important. Make sure all quotes, braces, and semicolons are in place. If you prefer, everything between braces can be placed on a single line.

# The Domain Name Service
CHAPTER 8

This /etc/named.conf configuration does not provide reverse lookup for its 192.168.42 subnet. However, it does reverse DNS lookup for the loopback subnet at 127.0.0 with zone "127.0.zone", which points to the file in the directory var/named specified in the options section. The solution to the reverse DNS problem is to provide a similar reverse DNS lookup for the 192.168.42 subnet. The following is a summary of how's done:

1. Add code in /etc/named.conf to /var/named/named.192.168.42.
2. Copy /var/named/127.0.zone to /var/named/named.192.168.42.
3. Modify /var/named/named.192.168.42 appropriately.
4. Restart named.

# Adding Code to /etc/named.conf

A zone must be created to handle reverse DNS queries for the domain's subnet. In this case, that subnet 192.168.42 will be named 192.168.42. This file must be pointed by the added zone in /etc/named.conf. If you haven't already, back up the /etc/named.conf, created by the Installation, using the following RCS commands:

```
ci /etc/named.conf
co -1 /etc/named.conf
```

Add the following lines to the bottom of /etc/named.conf:

```
zone 42.168.192.in-addr.arpa {
    type master;
    file "named.192.168.42";
}
```

This allows subnet 192.168.42/255.255.255.0 addresses to be resolved as names as instructed by the contents of zone data file /var/named/named.192.168.42.

# Creating and Modifying /var/named/named.192.168.42

First, copy /var/named/127.0.zone to /var/named/named.192.168.42.

> Note
Any time you modify a zone data file you must be sure to increment that file's serial number. The serial number is the first number after the first opening parenthesis and is usually expressed as yyyymmdd to give you 100 chances per day to increase it.

# Networking and Internet Services
PART II

Never use a serial number greater than 2147483647, as it will overflow the 32-bit internal representation of the serial number. This would produce a very hard to find bug, as your secondaries serials and won't update as needed. Frankly this will no longer be an issue by the year 2147, as compilers and operating systems will then accommodate much bigger numbers than 32 bits.

Obviously, serial numbers must never be more than ten digits, and must never include characters.

Failure to increment it will result in various slave and cache DNS servers failing to pick up your modifications. It must be incremented, not changed to a lesser value.

When you're creating a new dns zone file, the best practice is to set its serial number to the present date, revision 0. For example, if you create it on February 21, 2000, the serial number for the new file should be 200002210.

Listing 8.3 contains the installation default /var/named/127.0.0.zone file for new host, which you copied to /var/named/named.192.168.42 for modification.

# LISTING 8.3 The /var/named/named.192.168.42 File Before Modification

```
@ORIGIN 0.0.127-in-addr.arpa.

1D IN SOA localhost.root.localhost. (
42 ; serial (d. womans)
3H ; refresh
15M ; retry
1W ; expiry
1D ) ; minimum

1D IN NS localhost.
1D IN PTR localhost.
```

This is a typical reverse DNS zone file. The details will be discussed later in this chapter. What you need to do in change this file to resolve domain.cxm instead of localhost names.
