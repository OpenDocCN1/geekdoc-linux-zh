
## Overview of DNS and BIND

DNS gives your network an entry point into a hierarchical collection of hostname and IP address servers on an intranet or the Internet itself. All of the hosts on your network can query one or more local DNS servers for local hostname and IP address information. Requests for hostname and IP address information outside the administrative domain of your DNS servers are automatically-passed through the DNS chain until some DNS server can authoritatively give you the information you're looking for.

A common DNS misconception is that a system needs to run a DNS server to participate in DNS. This is not the case. Systems can be DNS clients without running a name server process. The client-side portion of the DNS system is known as a resolver, which is configured through the /etc/resolv.conf (which I will discuss later in this section). When a system participates in DNS all is configured through your system's Name Service Switch file, /etc/nwitch.conf, which is also discussed in detail later in this section.

Most hosts have traditional sources of hostname/IP address information, such as /etc/hosts files, as well as DNS servers. When an application needs to contact a specific host by name, your system goes through the following process:

1. It first checks the /etc/nswitch.conf hosts entry to determine how your system is configured to resolve hostnames and IP addresses. The /etc/nswitch (Name Service Switch) identifies the sequence in which files and network resources should be consulted to find a variety of information, including hostname/IP address information. The hosts entry generally looks something like the following:

hosts: files dns [NOTFOUND-RETURN] nis nisplus

The system on which this entry is used finds if not found in /etc/hosts file for information and then queries DNS. If the host is not found after querying DNS servers, the hostname/IP address lookup fails. Items in hosts entry after [NOTFOUND-RETURN] are not consulted, but are often left on this line as a reminder that they are valid values for hostname/IP address information. In this example, the NIS and NIS+ information sets would not be consulted.

### Tip
Some older applications still consult another configuration file called /etc/hosts.conf. This file provides similar information to that provided in /etc/nswitch.conf files about the order in which an /etc/hosts file and DNS should be consulted using the following entry:

```
order hosts.bind
```

The resolver functions in most recent versions of glibc /etc/nswitch.conf. However, if you have changed your /etc/nswitch.conf file and some specific application is consulting /etc/hosts and DNS in the wrong order, check your /etc/hosts.conf file. You may also report the problem to the current-maintainer of the program that you were running.

## Part III: Ubuntu System Administrators

2. Assuming the hostname or IP address of a specific host is not found in the /etc/hosts file, a system that is configured to consult DNS checks the contents of the text file /etc/resolv.conf to identify the DNS servers that it should consult, in order. This file also often contains information such as the default domain that should be queried when up non-fully qualified hostnames. For example, the /etc/resolv.conf on one of my Ubuntu systems looks like the following:

```
domain vonhagen.org
nameserver 0.0.0.0
nameserver 192.168.66.64
nameserver 208.67.222.222
nameserver 208.67.220.222
```

In this example, non-fully qualified hostnames as 64bit are assumed to be within the domain vonhagen.org. The name servers are queried in order until one responds or a maximum number of connection failures and associated retries have elapsed, in which case the query fails. The name servers 208.67.222.222 and 208.67.220.222 are public name servers from the folks at OpenDNS.com, which provide public name services and are well worth checking out! For a list of publicly available DNS servers all over the world, see www.serverlist.org.

### Tip
A name server specification of 0.0.0.0 is actually a shortcut for querying a local name server using the first IP address assigned to the local system. This is the loopback address, which is usually 127.0.0.1, but is not guaranteed to be. Using the shortcut 0.0.0.0 causes your request to be sent to an IP address that is known to be valid for the current host, whatever it may be.

3. When a DNS server responds, it first tries to resolve the query itself. DNS servers are configured through many specially formatted text files that are essentially anonymous to a domain or subdomain that the server can provide authoritative information for. If the hostname or IP address is present in a zone where the DNS server is authoritative for or if it is already present in the server's cache of previously answered requests, the DNS server will reply directly to the request. If the request is in a subdomain that the DNS server knows an authoritative server for information for, it will forward the request to that DNS server for resolution. The DNS server will then reply to the client.

4. If the DNS server reports cannot resolve the query in one way or another, it queries one of the Internet's top-level name servers (as root servers) to identify the name server that is responsible for the domain or the range of IP addresses that contains the IP address for which the application is looking for hostname information.

5. The root name server returns a pointer to the appropriate name server, which your system queries for hostname or IP address. If this name server is not actually authoritative for the domain, it may forward the query to other name servers.

## Chapter 32: Setting Up a DNS Server

forwarding is greatly invisible to you and most often occurs when querying subdomains rather than top-level domains. This combination of local, root, and hierarchical name servers is elegant in its simplicity. When your host finally receives the hostname or IP address it is looking for, it typically caches value so that subsequent requests for the same information won't go any further than the local name server.

BIND is generally configured in one of four ways:

- As a master server that is an authoritative source of DNS information for one or more zones
- As a caching-only server that is not authoritative for any zone, but that caches the results from DNS queries to minimize network traffic. Most Ubuntu Server systems will run at least a caching-only server
- As a resolver-only client that does not run a DNS server but whose DNS resolver is configured to consult name servers through its /etc/resolv.conf

Most desktop systems do not need to actually run a name server and will work fine as resolver-only clients. However, if you spend a vast amount of time surfing the Web or on a heavily loaded network, you might want to upgrade your system to running a caching-only client. DNS servers do not consume a vast amount of system resources, but they do require memory, process slots, and so on. If a system that you are configuring or using does not need to provide host information for a zone (which would mandate running a DNS server), only the user(s) of a system can determine which of the caching-only or resolver-only configurations works best for that.

### Installing a DNS Server

Although every Ubuntu system provides the basic client-side commands for querying and dynamically mapping hostnames to IP addresses, an actual DNS server is not installed as part of a default Ubuntu installation. Lets face it—not everybody needs to run a DNS server, and for small, home networks, maintaining your /etc/hosts files isn't that of an issue if you only have a few machines. However, if you want to run your own name server (which probably want to do if you are responsible for an enterprise network or SHO network with a relatively large number of hosts), the package management utilities provided on Ubuntu systems make it easy to install the BIND DNS server by installing the bind9 package. See Chapter 19, "Adding, Removing, and Updating Software," for more information about installing software on Ubuntu systems.
