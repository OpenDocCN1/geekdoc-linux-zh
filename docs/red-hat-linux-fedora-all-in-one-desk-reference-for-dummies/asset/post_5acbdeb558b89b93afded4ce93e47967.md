
## Chapter 5: Setting Up DNS and NIS
### In This Chapter
- ✔ Understanding DNS
- ✔ Learning about BIND
- ✔ Configuring DNS
- ✔ Setting up a caching name server
- ✔ Configuring a primary name server
- ✔ Understanding NIS
- ✔ Configuring NIS servers and clients
- ✔ Trying out NIS

Domain Name System (DNS) is an Internet service that converts a fully qualified domain name, such as www.redhat.com, into its corresponding IP address such as 216.148.218.195. You can think of DNS as the directory of Internet hosts — DNS is the reason why you can use easy-to-remember host names even though TCP/IP requires numeric IP addresses for data transfers. DNS is basically a hierarchy of distributed DNS servers. In this chapter, I provide an overview of DNS and show you how to set up a caching DNS server on your Red Hat Linux system.

Network Information System (NIS) is another client/server service designed to manage information shared among several host computers on a network. Typically, NIS maintains a common set of user accounts and other system files on a UNIX or Linux system for a group of hosts on a local area network (LAN). This service, among others, enables a user to log in on all hosts with the same username and password. This chapter briefly describes the NIS client and server software, and I show you how to use them on a Red Hat Linux system.

### Understanding Domain Name System (DNS)
In TCP/IP networks, each network interface (for example, an Ethernet card or a dial-up modem connection) is identified by an IP address. Because IP addresses are hard to remember, an easy-to-remember name is assigned to the IP address — much like the way a name goes with a telephone number. For example, instead of having to remember that the IP address of Red Hat's Web server is 216.148.218.195, you can simply refer to that host by its name, www.redhat.com. When you type www.redhat.com as the URL in a Web browser, the name www.redhat.com has to be translated into its corresponding IP address. This is where the concept of DNS comes in.

### What is DNS?
Domain Name System is a distributed, hierarchical database that holds information about computers on the Internet. That information includes host name, IP address, and mail-routing specifications. Because this information resides in many DNS hosts on the Internet, DNS is called a distributed database. The primary job of DNS is to associate host names to IP addresses and vice versa.

In ARPANET — the precursor to today's Internet — the list of host names and corresponding IP addresses was maintained in a text file named HOSTS.TXT, which was managed centrally and periodically distributed to every host on the network. As the number of hosts grew, this static host table quickly became unreasonable to maintain. DNS was proposed by Paul Mockapetris to alleviate the problems of a static host table. As formally documented in Request for Comment (RFC) 882 and 883 (published in November 1983, see www.faqs.org/rfcs/rfc882.html and www.faqs.org/rfcs/rfc883.html), the original DNS introduced two key concepts:
- Use of hierarchical domain names, such as www.ee.umd.edu and www.redhat.com
- Distributed responsibility for managing the host database by using DNS servers throughout the Internet

DNS as we know it today is an Internet standard documented in RFCs 1034 and 1035. The standard has been updated and extended by several other RFCs — 1101, 1183, 1348, 1876, 1982, 1996, 2065, 2181, 2136, 2137, 2308, 2535, 2845, and 2931. The earlier updates define data encoding, whereas later ones focus on improving DNS security. To read these and other RFCs online, visit Ohio State University's Internet RFC page at this Web address:

```
www.cis.ohio-state.edu/hypertext/information/rfc.html
```

DNS defines the following:
- A hierarchical domain-naming system for hosts.
- A distributed database that associates every domain name with an IP address.
- Library routines (resolvers) that network applications can use to query the distributed DNS database. (This library is called the *resolver library*.)
- A protocol for DNS clients and servers to exchange information about names and IP addresses.

Nowadays, all hosts on the Internet rely on DNS to access various Internet services on remote hosts. As you may know from personal experience, when you obtain Internet access from an Internet service provider (ISP), your ISP provides you with the IP addresses of name servers — the DNS servers your system accesses whenever host names have to be mapped to IP addresses.

If you have a small LAN, you may decide to run a DNS server on one of the hosts or to use the name servers provided by the ISP. For medium-sized networks works with several subnets, you can run a DNS server on each subnet to provide efficient DNS lookups. On a large corporate network, the corporate domain (such as microsoft.com) is further subdivided into a hierarchy of subdomains; several DNS servers may be used in each subdomain.

In the following sections, I provide an overview of the hierarchical domain-naming convention and describe BIND — the DNS software used on most UNIX systems, including Red Hat Linux.

### Learning hierarchical domain names
DNS uses a hierarchical tree of domains to organize the namespace — the entire set of names. Each higher-level domain has authority over its lower-level subdomains. Each domain represents a distinct block of the namespace and is managed by a single administrative authority. Figure 5-1 illustrates the hierarchical organization of the DNS namespace.

Figure 5-1:
The DNS namespace is organized in a hierarchy.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_698_0.png)

The root of the tree is called the root domain and is represented by a single dot (.). The top-level, or root-level, domains come next. The top-level domains are further divided into second-level domains, which, in turn, can be broken into further subdomains.

The top-level domains are relatively fixed and include well-known domains such as COM, NET, ORG, EDU, GOV, and MIL. These are the commonly used top-level domains in the United States. These top-level domains came about as the Internet came to widespread use in the early 1990s.

There is another set of top-level domain names for the countries. These domain names use the two-letter country codes assigned by the International Organization for Standardization (abbreviated as ISO; see www.iso.ch). For example, the top-level country code domain for the United States is US. In the United States, many local governments and organizations use the US domain. For example, mcps.k12.md.us is the domain name of the Montgomery County Public Schools in the state of Maryland, USA.

The fully qualified domain name (FQDN) is constructed by stringing together the subdomain names, from lower- to higher-level, using dots (.) as separators. For example, REDHAT.COM is a fully qualified domain name; so is EE.UMD.EDU. Note that each of these may also refer to a specific host computer. Figure 5-2 illustrates the components of a fully qualified domain name.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_699_0.png)

Domain names are case-insensitive. Therefore, as far as DNS is concerned, the domains UMD.EDU and umd.edu both represent University of Maryland's domain. The norm, however, is to type domain names in all lowercase.

### Exploring Berkeley Internet Domain Name (BIND)
Most UNIX systems, including Red Hat Linux, come with the BIND system — a well-known implementation of DNS. The BIND software is installed during Red Hat Linux installation, as long as you select the DNS Name Server package group when selecting the packages for installation.

To see which version of BIND is installed on your Red Hat Linux system, type the following command:

```
rpm -q bind
```

If BIND is installed, this command should display a line similar to the following with the version number of the RPM file:

```
bind-9.2.2-19
```

As this output shows, BIND Version 9.2.2 is installed on my system.

BIND includes three major components:
- The named daemon — the name server — that responds to queries about host names and IP addresses
- A resolver library that applications can use to resolve host names into IP addresses (and vice versa)
- Command line DNS utility programs (DNS clients), such as dig (Domain Internet Groper) and host that users can use to query DNS

I describe these components of BIND in the next few sections. In later sections, I explain how to configure the resolver and the name server.

### named — the BIND name server
The named daemon is the name server that responds to queries about host names and IP addresses. Based on the configuration files and the local DNS database, named either provides answers to queries or asks other servers and caches their responses. The named server also performs a function referred to as zone transfer, which involves copying data among the name servers in a domain.

The name server operates in one of three modes:
- Primary or Master — In this case, the name server keeps the master copy of the domain's data on disk. There is one primary server for each domain or subdomain.
- Secondary or Slave — A secondary name server copies its domain's data from the primary server using a zone transfer operation. You can have one or more secondary name servers for a domain.
- Caching — A caching name server loads the addresses of a few authoritative servers for the root domain and gets all domain data by caching responses to queries it has resolved by contacting other name servers. Primary and secondary servers also cache responses.
