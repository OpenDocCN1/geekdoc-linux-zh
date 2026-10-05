
# CHAPTER 10 NETWORKING AND THE INTERNET

### Table 10-4 Common daemons (continued)

| Daemon | Used for by | Function |
|---|---|---|
| nfsd, statd, lockd, mount quota | DNS | These five daemons operate to handle NFS (page 773) operations. The nfsd daemon handles file and directory requests. The statd and lockd implement network file and record locking. The mount daemon converts filesystem name requests from the mount utility into NFS handles and checks access permissions. If disk quotas are enabled, rquot handles those. |
| nptd | NTP | Synchronizes time on network computers. Requires a /etc/ntp file. For more information go to www.ntp.org. |
| portmap | RPC | Maps incoming requests for RPC services to TCP or UDP port numbers on the local system. Refer to “Network Services” on page 406. |
| pppd | PPP | For a modem, this protocol controls the pseudo-interface representing the IP connection between the local computer and a remote computer. Refer to “PPP: Point-to-Point Protocol” on page 381. |
| rexecd | rexec | Allows a remote user with a valid username and password to run programs on a system. Its use is generally deprecated for security reasons; consider programs, such as PC-based X servers, may not have an option. |
| routed | Routing tables | Manages the routing tables so your system knows where to send messages that are destined for remote networks. If your system does not have a /etc/defaultroute routed is started automatically to listen to incoming routing messages and advertise outgoing routes to other systems on the local network. A newer daemon, the gateway daemon (gated), offers enhanced reliability and support for routing protocols and is more complex. |
| rsyslog | System log | Transcribes important system events and stores them in files and forwards them to users or another host running the rsyslog daemon. This daemon is configured with /etc/rsyslog.conf. See page 625. |
| sendmail | Mail programs | The sendmail daemon from Berkeley Unix and has been available for a long time. The de facto mail transfer program on the Internet, the sendmail daemon always listens on port 25 for incoming mail connections and then calls a local delivery agent, such as /bin/mail. Mail user agents (MUAs), as KMail and Thunderbird, typically use sendmail to deliver mail messages. |

### Table 10-4 Common daemons (continued)

| Daemon | Used for by | Function |
|---|---|---|
| smbd, nmbd | Samba | Allow Windows PCs to share files and printers with UNIX and Linux computers (page 797). |
| ssh | ssh, scp | Enables secure logins between remote systems (page 676). |
| talkd | talk | Allows you to have a conversation with another user on the same or remote machine. The talkd daemon handles the connections between the machines. The talk utility on each system contacts the talkd daemon on the other system for a bidirectional conversation. |
| telnetd | TELNET | One of the Original Internet access protocols (page 391). |
| tftpd | TFTP | Used to boot a system or get information from a network. Examples include network computers, routers, and some printers. |
| timed | Time server | On a LAN synchronizes time with other computers that are also running timed. |
| xinetd | Internet superserver | Listens for service requests on network connections and starts up the appropriate daemon to respond to any particular request. Because of xinetd, a system does not need the daemons running continually to handle various network requests. For more information refer to page 464. |

## PROXY SERVERS

A proxy is a network service that is authorized to act for a system while not being part of that system. A proxy server or proxy gateway provides proxy services; it is a transparent intermediary, relaying communications back and between an application, as a browser and a server, usually outside of a LAN and frequently on the Internet. When more than one process uses the proxy gateway/server, the proxy must keep track of which processes are connecting to which hosts/servers so that it can return the messages to the proper process. The most commonly encountered proxies are email and Web proxies.

A proxy gateway isolates the local computer from all other computers or from specified domains by using at least two IP addresses: one to communicate the local computer and one to communicate with a server. The proxy server/gateway examines the header information on all packets handles that it can encode, route, and decode them properly. The difference between a proxy gateway and a proxy server is that the proxy server usually includes cache (page 1139) to store frequently used Web pages so that the next request for that page is available locally and quickly; a proxy gateway typically does not use cache. The terms “proxy server” and “proxy gateway” are frequently used interchangeably.

Proxy servers/gateways are available for such common Internet services as HTTP, FTP, SMTP, and SNMP. When an HTTP proxy sends queries from local systems, it presents a single organization IP address (the external IP of the proxy server/gateway) to all servers. It funnels all user requests to the appropriate servers and keeps track of them. When the responses come back, the HTTP proxy fans them out to the appropriate applications using each machine's unique IP address, thereby protecting local addresses from remote/specified servers.

Proxy servers/gateways are generally just part of an overall firewall strategy to prevent intruders from stealing or damaging an internal network. Other functions, which can be either combined with or kept separate from the proxy server/gateway, include packet filtering, which blocks traffic based on origin and type, and user activity reporting, which helps management learn how the Internet is being used.

## RPC NETWORK SERVICES

Much of the client/server interaction over a network is implemented using the RPC (Remote Call) protocol, which is implemented as a set of library calls that make network access transparent to the client and server. RPC specifies and interprets messages but does not concern itself with protocols; it runs on top of TCP/IP or UDP/IP. Services that use RPC include NFS. RPC was developed by Sun as ONC RPC (Open Computing Remote Procedure Call) and differs from Microsoft RPC.

In the client/server model, a client contacts a server on a specific port (page 401) to avoid any mixup between services, clients, and servers. To maintain a long list of port numbers and to enable new clients/servers to start without registering a port number with a central registry, when a server uses RPC, it specifies the port it expects to be contacted on. RPC servers typically use port numbers that have been defined by Sun. If a server does not use a predefined port, it picks an arbitrary number.

The server registers itself with the RPC portmapper (**portmap daemon**) on the local system. The server tells the daemon what port it is listening on. The client contacts the RPC portmapper to find the port of the desired service. The portmapper returns the port number to the client. The client then contacts the server on that port. The server registers itself with the RPC portmapper (**portmap daemon**) on the local system. The portmap daemon listens for registration requests from RPC servers. Through these exchanges, **portmap** learns the location of every RPC service. The portmap daemon listens on port requests. The **portmap** file (page 496) maps services to ports. **/etc/services** (page 497) lists the RPC services. The sequence of events for communication occurs as follows:

- 1. The client program makes an RPC call to obtain data from the server. (The filesystem receives the request.)
- 2. The client contacts the portmapper to find the port of the desired service (the filesystem).
- 3. The portmapper returns the port number to the client. (The filesystem receives the request.)
- 4. The client contacts the server on that port. (The filesystem receives the request.)
- 5. The server responds to the client. (The result is returned.)
- 6. The RPC libraries on the remote server return the result to the calling program.

Under Ubuntu Linux servers start and run their own daemons. When RPC servers are started by xinetd (page 464), the portmap daemon must be started. The init scripts (page 440) make sure portmap starts before xinetd. You can confirm this sequence by looking at the numbers associated with /etc/rc.d/*/portmap and /etc/rc.d/*/xinetd. If the portmap daemon stops, you must restart all RPC servers on the system.

## USENET

Of the earliest information services available on the Internet, Usenet is an electronic bulletin board that allows users with common interests to exchange information (commonly referred to as netnews). It was formed in 1979 by a few sites decided to share some software and information on topics of common interest. They agreed to contact one another and to pass information over dial-up telephone lines (at that time running at 1,200 baud at best), using UNIX's uu (UNIX-to-UNIX copy program).

The popularity of Usenet led to many changes in usenet to handle the escalating usage of messages and sites. Today most of news flows over network links using a sophisticated protocol designed specifically for this: NNTP (Network News Transfer Protocol). The news messages are stored in a standard format, and the many public domain archives allow you to read. An old, simple interface is named readers. Other interfaces, such as rm, its Window System cousin xr, tin, and wv, have many features that allow you to browse and reply to the articles that are available or create articles of you. In addition, Netscape and Mozilla include an interface that you can use to read news (Netscape/Mozilla News) as part of your Web browsers. One of the easiest ways to read netnews is to go to groups.google.com. The program you select to read netnews is largely a matter of personal taste.
