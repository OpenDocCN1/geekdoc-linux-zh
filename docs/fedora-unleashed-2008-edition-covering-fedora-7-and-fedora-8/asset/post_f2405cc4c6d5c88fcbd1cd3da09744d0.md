
When you have your ACL lines in place, you can put together appropriate `http_access` lines. For example, you might want to use a multilayered access system so that certain users (for example, company directors) have full access, whereas others are filtered. For example:

```
http_access allow directors
http_access deny hotmail
http_access deny zipfiles
http_access allow internal lunchtimes
http_access deny all
```

Because Squid matches those lines in order, directors will have full, unfiltered access to the web. If the client IP address is not in the `directors` list, the two `deny` lines are processed so that the user cannot download `.zip` files or read online mail at Hotmail. After blocking those two types of requests, the `allow` on the fourth line allows internal users to access the web, as long as they do so only at lunch time. The last line (which is highly recommended) blocks all other users from the proxy.

## Reference

- `http://www.squid-cache.org/`—The home page of the Squid Web Proxy Cache.
- `http://www.deckle.co.za/squid-users-guide/Main_Page`—The home page of *Squid: A User's Guide*, a free online book about Squid.
- `http://www.faq.org/docs/securing/netproxy-squid.html`—A brief online guide to configuring a local Squid server.
- `http://squid.visolove.com/squid/index.htm`—The home page of a company that can provide commercial support and deployment of Squid.
- `http://squid.visolove.com/squid/reverseproxy.htm`—ViSolve's guide to setting up Squid to reverse proxy to cache a local web server for external visitors.

As well as these URLs, there are two excellent books on the topic of web caching. The first is *Squid: The Definitive Guide* (O'Reilly) by Duane Wessel, ISBN: 0-596-00162-2. The second is *Web Caching* (O'Reilly) also by Duane Wessel, ISBN: 1-56592-536-X.

Of the two, the former is more practical and covers the Squid server in depth. The latter is more theoretical, discussing how caching is implemented. Wessel is one of the leading developers on Squid, so both books are of impeccable technical accuracy.

## CHAPTER 23
# Managing DNS

Computers on a network need to be useful, which means you need to be able to identify each computer so that you can connect to and communicate with it. Most of today’s networks use the *Internet Protocol* (*IP*), so each computer on this network has a unique IP address to identify it.

An IP address is a very large 32-bit number, but there is a shortcut method of displaying that number called the *dotted-quad address*. The dotted-quad form of the address is made of four 8-bit numbers separated by dots. For example, a computer with the address 3232250992 has the dotted-quad form 192.168.60.112. It’s easier to use and remember the dotted-quad form of an IP address, but even then, remembering a lot of numbers becomes quite difficult. The *domain name system* (*DNS*) enables you to allocate host-names that are much easier to remember to these IP addresses. These names, such as fedoraproject.org, are translated by DNS into the dotted-quad IP address, saving time—and memory!

This translation process is called *name resolution* and is performed by software known as a *resolver*. For the average user, local configuration involves the DNS client, which queries a remote DNS server to exchange information. The DNS servers are typically maintained by *Internet service providers* (*ISPs*) and large corporate networks, although anyone can configure and run his own DNS server. All computers on networks need to have a properly configured DNS client.

This chapter introduces DNS concepts and practice using *Berkeley Internet Name Domain* (*BIND*), the de facto standard DNS software for UNIX. In this chapter, you learn some of the concepts that are basic to DNS and its functions, including how DNS structure information is stored, how DNS serves name information to users, and how name resolution actually works. You learn how to use BIND to configure nameservers and how to provide DNS for a domain. This chapter also teaches you some important techniques for keeping DNS functions secure, as well as some of the most important troubleshooting techniques for tracking down potential problems related to your DNS functions.

If you are not going to be a DNS administrator, much of the information in this chapter will be of no practical use to you. That said, the knowledge of DNS that you can gain in this chapter might help you understand DNS problems that occur—so you will realize that it is not your computer that is broken! You will also see how, after you register a domain name, you can obtain third-party DNS service so that you do not have to maintain a DNS server. Also, the commonly used DNS-related tools are explained with a focus on how they can be used to troubleshoot domain name resolution problems that you're likely to encounter.

DNS is essential for many types of network operations, and especially so when your network provides connectivity to the outside world via the Internet. DNS was designed to make the assignment and translation of hostnames fast and reliable and to provide a consistent, portable namespace for network resources. Its database is maintained in a distributed fashion to accommodate its size and the need for frequent updates. Performance and bandwidth utilization are improved by the extensive use of local caches. Authority over portions of the database is delegated to people who are able and willing to maintain the database in a timely manner, so updates are no longer constrained by the schedules of a central authority.

DNS is a simple—but easily misconfigured—system. Hostname resolution errors might manifest themselves in ways that are far from obvious, long after the changes that caused the errors were made. Such naming errors can lead to unacceptable and embarrassing service disruptions.

An understanding of the concepts and processes involved in working with BIND will help to make sure that your experiences as a DNS manager are pleasant ones.

### IN THIS CHAPTER

- Configuring DNS for Clients
- Essential DNS Concepts
- Using DNS Tools
- Configuring a Local Caching Nameserver
- Your Own Domain Name and Third-Party DNS
- Providing DNS for a Real Domain with BIND
- Providing DNS for a Real Domain
- Troubleshooting DNS
- Managing DNS Security
- Reference

## Configuring DNS for Clients

Later in the chapter, we focus on setup and configuration to provide DNS. This section briefly examines the setup and configuration required for a computer to use DNS services. The important user setup and configuration processes for DNS are likely to have been accomplished during the initial installation of Fedora. After the initial installation, further DNS configuration can be accomplished by one or more of these methods:

- Using Dynamic Host Control Protocol (DHCP), in which case some system settings are updated by the dhclient command without intervention by a local or remote administrator or user
- Using the system-config-network GUI configuration tool
- Manually editing the system's `/etc/host.conf` configuration file to specify the methods and order of name resolution
- Manually editing the system’s /etc/nsswitch.conf configuration file to specify the methods and order of name resolution
- Manually editing the system’s /etc/hosts file, which lists specific hostnames and IP addresses
- Manually editing the system’s /etc/resolv.conf configuration file to add name-server, domain, or search definition entries

Successful DNS lookups depend on the system’s networking being enabled and correctly configured. You can learn more about how to accomplish that in Chapter 14, “Networking.”

When an application needs to resolve a hostname, it calls system library functions to do the name resolution. If the GNU C library installed is version 2 or later, the /etc/nsswitch.conf configuration file is used. Older versions of the library use /etc/host.conf. Fedora uses the newer GNU C library, but /etc/host.conf is still provided for applications that have been statically linked with other libraries. The two files should be kept in sync.

### The /etc/host.conf File

The /etc/host.conf file, known as the resolver configuration file, specifies which services to use for name resolution and the order in which they are to be used. This file has been superseded by /etc/nsswitch.conf, but is still provided for applications that use other libraries.

By default with Fedora, this file contains the following:

```
order hosts,bind
```

The order shown here is to first consult /etc/hosts for a hostname. If the hostname is found in /etc/hosts, use the IP address specified there. If the hostname is not found in /etc/hosts, try to resolve the name with DNS (BIND).

One other option is available, although it is not set by default. This is NIS, which is Sun’s Network Information Service.

### The /etc/nsswitch.conf File

The file /etc/nsswitch.conf is the system databases and name service switch configuration file. It contains methods for many types of lookups, but here we are concerned with DNS resolution, so the line we are interested in is the hosts line. This line defines the methods to be used for resolving hostnames and the order in which to apply them. The methods used are the following:

- db—Local database files (*.db)
- files—Use the local file /etc/hosts
- dns—Use BIND
