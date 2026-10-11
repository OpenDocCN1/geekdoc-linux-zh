
router along the way and an acknowledgment to get back. You can put this information to good use when you are trying to identify the location of a network bottleneck.

The traceroute utility has no concept of the path from one host to the next; instead, it simply sends out packets with increasing TTL (time to live) values. TTL is an IP header field that indicates how many more hops the packet should be allowed to make before being discarded or returned. In the case of a traceroute packet, the packet is returned by the host that has the packet when the TTL value is zero. The result is a list of hosts that the packet traveled through to get to its destination.

The traceroute utility can help you solve routing configuration problems and locate routing path failures. When you cannot reach a host, use traceroute to discover what path the packet follows, how far it gets, and what the delay is.

The next example shows the output of traceroute when it follows a route from a local computer to www.linux.org. The first line indicates the IP address of the target, the maximum number of hops that will be traced, and the size of the packets that will be used. Each numbered line contains the name and IP address of the intermediate destination, followed by the time it takes a packet to make a trip to that destination and back again. The traceroute utility sends three packets to each destination; thus three times appear on each line. Line 1 shows the statistics when a packet is sent to the local gateway (less than 3 milliseconds). Lines 4-6 show the packet bouncing around Mountain View (California) before it goes to San Jose. Between hops 13 and 14 the packet travels across the United States (San Francisco to somewhere in the East). By hop 18 the packet has found www.linux.org. The traceroute utility displays asterisks when it does not receive a response. Each asterisk indicates that traceroute has waited three seconds. Use traceroute6 to test IPv6 networks.

```
$ /usr/sbin/traceroute www.linux.org
traceroute to www.linux.org (198.182.196.56), 30 hops max, 38 byte packets
1 gw.localco.com (204.94.139.65) 2.904 ms 2.425 ms 2.287 ms
2 covad-gw2.meer.net (209.157.140.1) 19.727 ms 23.287 ms 24.783 ms
3 gw-mv1.meer.net (140.174.164.1) 18.795 ms 24.973 ms 19.207 ms
4 di-4-2.a02.mtwca01.us.ra.verio.net (206.184.210.241) 59.091 ms d1-0-0-a-200.a03.mtwca01.us.ra.verio.net (206.86.206.25) 54.948 ms 39.485 ms
5 fa-11-0-0.a01.mtwca01.us.ra.verio.net (205.184.188.1) 40.182 ms 44.405 ms 49.362 ms
6 p1-1-0-0.a09.mtwca01.us.ra.verio.net (205.149.170.66) 78.688 ms 66.266 ms 28.003 ms
7 p1-12-0-0.a01.snjsca01.us.ra.verio.net (209.157.181.166) 32.424 ms 94.337 ms 54.946 ms
8 f4-1-0.sj0c.verio.net (129.250.31.81) 38.952 ms 63.111 ms 49.083 ms
9 sj0cqu0.verio.net (129.250.3.98) 45.031 ms 43.496 ms 44.925 ms
10 mae-west1.US.CRL.NET (198.32.136.10) 48.525 ms 66.296 ms 38.996 ms
11 t3-ames1.sfo-us.crl.net (165.113.0.249) 138.808 ms 78.579 ms 68.699 ms
12 E0-CRL-SF0-E0-E0X0.US.CRL.NET (165.113.153.2) 43.023 ms 51.910 ms 42.967 ms
13 sf02-vaal.ATM.us.crl.net (165.113.0.254) 135.551 ms 154.606 ms 178.632 ms
14 mae-east-02.ix.ai.net (192.41.17.207) 158.351 ms 201.811 ms 204.560 ms
15 ocl12-3-0-0.mae-east.ix.ai.net (205.134.161.2) 202.851 ms 155.667 ms 219.116 ms
16 border-ai.involvic.com (205.134.175.254) 214.622 ms 190.423 ms
17 router.involic.com (198.182.196.1) 224.378 ms 235.427 ms 228.856 ms
18 www.linux.org (198.182.196.56) 207.964 ms 178.683 ms 179.483 ms
```

## host AND dig: QUERY INTERNET NAMESERVERS

The host utility looks up an IP address given a name, or vice versa. The following example shows how to use host to look up the domain name of a machine, given an IP address:

```
$ host 64.13.141.6
6.141.13.64.in-addr.arpa domain name pointer ns.meer.net.
```

You can also use host to determine the IP address of a domain name:

```
$ host ns.meer.net
ns.meer.net. has address 64.13.141.6
```

The dig (domain information groper) utility queries DNS servers and individual machines for information about a domain. A powerful utility, dig has many features that you may never use. It is more complex than host.

Chapter 24 on DNS has many examples of the use of host and dig.

## jwhois: LOOKS UP INFORMATION ABOUT AN INTERNET SITE

The jwhois utility replaces whois and queries a whois server for information about an Internet site. This utility returns site contact and InterNIC or other registry information that can help you track down the person who is responsible for a site: Perhaps that person is sending you or your company spam (page 1107). Many sites on the Internet are easier to use and faster than whois. Use a browser and search engine to search on whois or go to www.networksolutions.com/whois or www.ripe.net/perl/whois to get started.

When you do not specify a whois server, jwhois defaults to whois.internic.net. Use the -h option to jwhois to specify a different whois server. See the jwhois info page for more options and setup information.

To obtain information on a domain name, specify the complete domain name, as in the following example:

```
$ jwhois sobell.com
[Querying whois.internic.net]
[Redirected to whois.godaddy.com]
[Querying whois.godaddy.com]
[whois.godaddy.com]
The data contained in Go Daddy Software, Inc.'s whois database,
...
Registrant:
Sobell Associates Inc
POBox 460068
San Francisco, California 94146-0068
United States
```

Registered through: GoDaddy.com
Domain Name: SOBEL.COM
Created on: 07-Apr-95
Expires on: 08-Apr-13
Last Updated on: 16-Jan-04

Administrative Contact:
Sobell, Mark sobell@meer.net
Sobell Associates Inc
PO BOX 460068
SAN FRANCISCO, California 94146-0068
United States
9999999999
Fax -- 9999999999

Technical Contact:
hostmaster@meer.net
meer.net
po box 390804
Mountain View, California 94039
United States
18888446337
Fax -- 18888446337

Domain servers in listed order:
NS.MEER.NET
NS2.MEER.NET

Several top-level registries serve various regions of the world. You are most likely to use the following ones:

| Registry | Address |
|---|---|
| North American registry | whois.arin.net |
| European registry | www.ripe.net |
| Asia-Pacific registry | www.apnic.net |
| U.S. military | whois.nic.mil |
| U.S. government | www.nic.gov |

## DISTRIBUTED COMPUTING

When many similar systems are found on the same network, it is often desirable to share common files and utilities among them. For example, a system administrator might choose to keep a copy of the system documentation on one computer's disk and to make those files available to remote systems. In this case, the system administrator configures the files so users who need to access the online documentation are not aware that the files are stored on a remote system. This type of setup, which is an example of distributed computing, not only conserves disk space but also allows you to update one central copy of the documentation rather than tracking down and updating copies scattered throughout the network on many different systems.

![](img/f28adb66a7398a382f0505e0ba74a872_424_0.png)

### Figure 10-2 A fileserver

Figure 10-2 illustrates a *fileserver* that stores the system manual pages and users’ home directories. With this arrangement, a user’s files are always available to that user — no matter which system the user logs in on. Each system’s disk might contain a directory to hold temporary files as well as a copy of the operating system. Chapter 22 contains instructions for setting up NFS clients and servers in networked configurations.

## THE CLIENT/SERVER MODEL

The client/server model was not the first computational model. First came the mainframe, which follows a one-machine-does-it-all model. That is, all the intelligence resides in one system, including the data and the program that manipulates and reports on the data. Users connect to a mainframe using terminals.

With the introduction of PCs, file-sharing networks became available. In this scheme data is downloaded from a shared location to a user’s PC, where a program then manipulates the data. The file-sharing model ran into problems as networks expanded and more users needed access to the data.

In the client/server model, a client uses a protocol, such as FTP, to request services, and a server provides the services that the client requests. Rather than providing data files as the file-sharing model does, the server in a client/server relationship is a database that provides only those pieces of information that the client needs or requests.

The client/server model dominates UNIX and Linux system networking and underlies most of the network services described in this book. FTP, NFS, DNS, email, and HTTP (the Web browsing protocol) all rely on the client/server model. Some servers, such as Web servers and browser clients, are designed to interact with specific utilities. Other servers, such as those supporting DNS, communicate with one another, in addition to answering queries from a variety of clients. Clients and servers can reside on the same or different systems running the same or different operating systems. The systems can be proximate or thousands of miles apart. A system that is a server to one system can turn around and act as a client to another. A server can reside on a single system or, as is the case with DNS, be distributed among thousands of geographically separated systems running many different operating systems.

The peer-to-peer (PTP) model, in which either program can initiate a transaction, stands in contrast to the client/server model. PTP protocols are common on small
