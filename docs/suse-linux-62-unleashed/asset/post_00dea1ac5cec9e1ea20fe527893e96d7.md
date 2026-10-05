
# Networking and Internet Services
PART II

## TABLE 8.1 Glossary of Essential DNS Terminology

| Term | Definition |
| :--- | :--- |
| Slave | An nameserver with authority for a zone that derives its data from another nameserver in a zone transfer. The other nameserver can be a master or another slave. If the information is derived, it is stored locally so it can function even if its source goes down. Note that a nameserver can be master for some zones, and for others. |
| Secondary Zone transfer | A synonym for *slave*. A transfer of zone data from a master or slave DNS server to a slave server. The receiving slave initiates the zone transfer after exceeding the refresh time or upon notification from the sending server that the data has changed. |

# DNS Maps Names to IP Numbers and Vice Versa

DNS maps names to IP numbers and vice versa. That's all it does. This is a vital concept to understand.

Almost everything you can do with a fully qualified domain name, URL, or any other name resolvable to an IP address, you can do with that IP address. And if you use IP addresses, you needn't use DNS (except for a few reverse DNS situations). For the most part, if a command doesn't work with the IP address, the fault is not with DNS but with a lower-level network function. Trying commands with IP addresses instead of domain names and URLs is a great troubleshooting test.

# The Forward and Reverse Zones Must Be Kept in Sync

The forward and reverse zones must be kept in sync. If a host changes IP addresses, that fact must be recorded in both the forward and the reverse zone data files and the serial number for each incremented. Failure to keep forward and reverse zones in sync can cause a variety of hard to solve problems, possibly world wide.

# The HUP Signal Versus Restart

According to most literature, including the named man page, named can be forced to reload its zone data files by the following command:

```
# HUP cat /var/run/named.pid
```

Unfortunately, this doesn't always work. A test that doesn't do what the troubleshooter thinks it does can waste hours. Therefore, the recommended way to get the zone data files to reload is with a restart:

```
# /sbin/init.d/named restart
```

# The Domain Name Service
CHAPTER 8

Restarting loses accumulated cache and eliminates DNS service during the restart process (20 seconds to minutes). If that is unacceptable, you can try the HUP signal, but be very careful to verify that it does what you think it will. You can view the current named database cache by sending an INT signal. This is explained in the section “Troubleshooting and Debugging DNS,” later in this chapter.

I have occasionally seen the behavior where there was no apparent reason in the logs for named not to restart, or however simply didn't. In this case, you can simply start it afresh (making sure, as mentioned earlier in the chapter, to look for errors in the log):

```
# /sbin/init.d/named
```

# The IN-ADDR.ARPA Domain

All reverse mappings exist in the IN-ADDR.ARPA domain, by eliminating any possible confusion regarding the number's purpose. The network and subnetwork parts of the IP address are placed in reverse order to follow the standard domain name as are written. Domain names describe the hostname, the subnetwork, and then the network, whereas IP addresses describe the network, the subnetwork, and finally the hostname. Placing the IP address in reverse order follows the convention established by the actual host and network names.

# Host Naming Schemes

It is common for sites to pick a naming scheme for all of their hosts. This tends to make it easier to remember names, especially as the site grows in size. For example, the east wing of the office might use famous music bands to name their machines, and the west wing might use the names of Star Trek characters. This also makes it easier to locate a machine by its name. Selecting a naming scheme can be a highly personal matter. One Linux company’s machine names are named after the number of the chemical element they (for example, xxx.xxx.xxx.2 would be named helium; xxx.xxx.xxx.8 would be named oxygen). Another Linux company names their hosts after Soul Cough songs.

# Configuring the DNS Client: /etc/resolv.conf

This is a more detailed explanation of material covered earlier. Every machine in your network is a DNS client. Each DNS client runs resolver code to query DNS servers. The resolver gets its configuration from /etc/resolv.conf. This file should look like the following:

```
search domain.com
nameserver 192.168.1.1
```

# Networking and Internet Services
PART II

The resolver gets its configuration from /etc/resolv.conf. This file should look like the following:

```
search domain.com
nameserver 192.168.1.1
```

# The Order Statement

A client can choose its method of name resolution or specify a hierarchy of methods to use. This is done with the order statement. This has two advantages:

- A /etc/hosts lookup is very fast.
- The computer can lookup when DNS is down.

To accomplish this, make sure the following line is in /etc/hosts:

```
order hosts,bind
```

# The Software of DNS

To configure DNS for your site, you need to be familiar with the following tools:

- named
- The resolver library
- nslookup
- traceroute

# named

The named daemon needs to run on DNS servers to handle queries. If named cannot answer a query, it forwards the request to a server that can. Along with queries, named is responsible for performing zone transfers. Zone transferring is the method by which DNS information is propagated across the Internet. If you didn't install the named daemon with the SuSE 6.2 operating system, you need to install it from the BIND distribution, available from http://www.suse.com. It is also on the CD-ROM that comes with this book. The filename is

```
bind-8.1.2-60.i386.rpm
```

The named daemon is normally started at bootup. The following are the commands to manually start, stop, and restart named, respectively:

- /sbin/init.d/named start
- /sbin/init.d/named stop
- /sbin/init.d/named restart

After you make any change to /etc/named.conf or any of the files referenced by named.conf, you must restart named before the changes will take effect.

# The Resolver Library

The resolver library enables client programs to perform DNS queries. This library is built into the standard library under Linux. The resolver library takes its configuration information from /etc/resolv.conf.

# nslookup

The nslookup command is a utility invoked from the command line to ensure that both the resolver and DNS server being queried are configured correctly. This does by resolving either a hostname to an IP address or an IP address into a domain name. To use nslookup, simply provide the address you want to resolve as a command line argument. For example, the following is one argument version:

```
# nslookup mtx.domain.com
```
