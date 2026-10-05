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

The resolv.conf file configures the DNS client, not the DNS server, even though in many cases they coexist on the same computer. The first line of resolv.conf defines domain.cxm as the client's default domain. The domain that's appended to machine names. The second line defines the IP address of the DNS server used by the client.

SuSE Linux 6.2 contains a lengthy default /etc/named.conf file used to demonstrate the use of the various parameters.

In this file, anything preceded by // or enclosed in /** */ is a comment. In English, the named.conf file says the following:

+   * All zone data files mentioned in named.conf shall be relative to directory
var/named.

+   * " is the root of the zone tree, hints to which are given in file named.ca, which is a list of the root servers.

+   * Any IP address in subnet 127.0.0.0 shall be resolved according to zone data file 127.0.0.zone, which is used, but not created, by the DNS server. Had it been it type slave instead of type master,* the file would have been created by the DNS server out of data from a zone transfer from a master zone on another computer.

When you're working with named.conf, remember that syntax is important. Make sure all quotes, braces, and semicolons are in place. If you prefer, everything between braces can be placed on a single line.