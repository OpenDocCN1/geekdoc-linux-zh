
# UNIX SYSTEM MANAGEMENT PRIMER PLUS

You can use and and and to combine filters. In the preceding example, you could limit the traffic to flowing to from apple.example.com on port 22 (SSH) as follows:

```
# tcpdump host apple.example.com and port 22
kernel filter, protocol ALL, datagram packet socket
tcpdump: listening on all devices
12:21:03.343382 eth0 > apple.example.com.ssh > 192.168.0.100:3662 P 412693775
41239383(108) ack 243160235 win 580 (DF) [tos 0x10]
12:21:03.363660 eth0 > apple.example.com.ssh > 192.168.0.100:3662 P 108:264(1
56) ack 1 win 580 (DF) [tos 0x10]
12:21:03.363660 eth0 < 192.168.0.100:3662: apple.example.com.ssh.: 1:1(0) ac
k 264 93888 (DF)
```

![](img/894492738e879267320b8d6f9a044180_167_0.png)

If you have a switched network (using a switch instead of a hub), you only see network traffic to and from the server on which tcpdump is run. A shared network configuration using a hub would show traffic from all devices on the hub.

If you are interested in the actual contents of the packets, you can use the -a flag to print out each packet in ASCII format. Note that the -a flag does not just print the data inside the packet—it prints the data that actually up the network transport protocols. Nevertheless, you should be able to make out any data that is not encrypted. You must also specify the snaplen, which is the maximum number of bytes that tcpdump is to take from each packet. The default is 68, which is not enough to show you any relevant data beyond the protocols themselves. In most cases, you can safely set snaplen anywhere from 1024 to 8192.

# Service Monitoring

During the Internet boom in the late 1990s, an increasing number of companies offering services such as email, dial-services, and news feeds. In this environment, system administrator could be tasked with determining if the company's servers were up and running. As a system administrator, your monitoring routine must include service monitoring.

The most significant benefit of service monitoring is its proactive nature; it probes for failures, rather than waiting for them to happen. Naturally, some services fail without warning, so service monitoring is reactive. In optimum circumstances, service monitoring alerts you to problems before they become noticeable to your customers.

Service monitoring can reveal even the smallest problems in a large Unix system; a glitch in a minor dependency, for example, can cause the service monitoring test to fail. Service monitoring processes can be made more powerful by implementing timeouts, which enable you to test how effectively your service is performing. The following sections discuss service monitoring techniques, some common services that can be monitored, what to look out for in the results, and how to tune each type of monitor. These tips should be applicable to any service monitoring software you are using.

# Monitoring Port Connections

A very basic method for service monitoring is to make sure the monitoring tool can connect to the network port service is listening on. If the monitoring tool can establish a connection, then the service must be running. A list of common services and their ports are listed in Table 6.1.

TABLE 6.1 Common Network Services and Their Port Numbers

| Service | Transport | Port |
|---|---|---|
| FTP | TCP | 21 |
| SSH | TCP | 22 |
| Telnet | TCP | 23 |
| SMTP | TCP | 25 |
| DNS | UDP, TCP | 53 |
| Finger | TCP | 79 |
| HTTP | TCP | 80 |
| POP | TCP | 110 |
| NNTP (news) | TCP | 119 |
| HTTPS | TCP | 443 |

> A Comprehensive List of Services
> You can find the list of network services your server knows about /etc/services, which maps service names to ports and protocols, much like Table 6.1. The official list of Internet services is available from RFC 1340, Assigned Numbers, at http://www.fags.org/rfc/rfc1340.html.

An ability to establish a connection indicates that something is listening on that port, but it doesn't guarantee that the service you've connected to is running correctly. The best service monitoring tools test services by subjecting them to use that simulates that of a real user. These types of monitoring tools attempt to send and retrieve mail from a mail server, dial out modems and authenticate to your network, and post articles to newsgroups. In each case, if the service can't perform the attempted action, the service fails the test. This kind of testing establishes a service's usability, as opposed to its availability.

# Monitoring the POP (Post Office Protocol)

System administrators commonly monitor the POP, or Post Office Protocol, service. POP is used to access mailboxes. In this example, you see that POP is failed. Here's an example of the:

```
SERVER -OK (version3)
CLIENT user
SERVER -ERR password required
CLIENT password
SERVER -ERR authentication failed
```

In this example, you see that the request resulted in an error—when it happens, the client is automatically disconnected. To test this, you must determine whether the server is functioning.

```
SERVER -OK (version3)
CLIENT user
SERVER -ERR password required
CLIENT password
SERVER -OK
```

If you can see that the server is functioning.

# Monitoring the Domain Name Service

The Domain Name Service (DNS) is another common service, without which the Internet wouldn't function. Unlike POP, DNS provides many functions, including name resolution, address caching, forwarding, and zone transfers. DNS conducts most communication using UDP, and in binary format; therefore, DNS does not give us a simple to work with.

In addition to a more complex service than POP, DNS also provides numerous features. Perhaps the most useful of these features is name resolution. To test name resolution, you must determine whether the name server can successfully resolve a name into an IP address (or vice versa)—if it can, then the server is working.

All of the monitoring software discussed later in this chapter will monitor name servers; you can also try this on your own. To perform the test, you must first decide which address to query.

# Choose an Established Address for Reliable Results

When monitoring DNS resolution performance, choose a well-established address—you are depending on a third party for your monitoring, and if that third party's DNS servers are unreliable, your monitoring results are just as.

One example of a well-established, reliable address is that of Yahoo!. To run the test, query for www.yahoo.com When you run the query manually, you see the following result (as of the time of writing):

```
nslookup www.yahoo.com
Server: stiffnessit.targetx.com
Address: 192.168.1.23
Non-authoritative answer:
Name: www.yahoo.com
Addresses: 64.58.76.179, 64.58.76.222, 64.58.76.223, 64.58.76.224, 64.58.76.225
64.58.76.226, 64.58.76.227, 64.58.76.228
Aliases: www.yahoo.com
```

This lists a lot of different addresses, but you are only concerned that you get a valid response from your name server—if it responds with results, you assume that the server is working correctly. However, if you actually compare the results to a known list of addresses, you run the risk of Yahoo! changing addresses behind your back at any time, triggering false alarms.
