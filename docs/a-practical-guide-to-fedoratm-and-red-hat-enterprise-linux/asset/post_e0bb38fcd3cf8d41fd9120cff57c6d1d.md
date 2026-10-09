
## Common daemons (continued)

| **Daemon** | **Used for or by** | **Function** |
| --- | --- | --- |
| **radvd** | IPv6 | IPv6 Router Advertisement Daemon. Provides autoconfiguration on the network if the local system is being used as a router. |
| **rpcbind** | RPC | Maps incoming requests for RPC service numbers to TCP or UDP port numbers on the local system. Refer to “RPC Network Services” on page 317. |
| **rsyslogd** | System log | Transcribes important system events and stores them in files and/or forwards them to users or another host running the **rsyslogd** daemon. See page 620. |
| **sendmail** | Mail programs | The **sendmail** daemon came from Berkeley UNIX and has been available for a long time. The *de facto* mail transfer program on the Internet, the **sendmail** daemon always listens on port 25 for incoming mail connections and then calls a local delivery agent, such as **/bin/mail**. Mail user agents (MUAs), such as KMail and Thunderbird, typically use **sendmail** to deliver mail messages. See also **exim4**. See page 739. |
| **smartd** | SMART Disk Monitoring Daemon | Monitors the Self-Monitoring, Analysis and Reporting Technology (SMART) system built into many hard drives. SMART tests drive reliability, predicts failure, and performs other self tests. Part of the **smartmontools** package. See page 82. |
| **smbd**, **nmbd** | Samba | Allow Windows PCs to share files and printers with UNIX and Linux computers. See page 827. |
| **sshd** | *ssh*, *scp* | Enables secure logins between remote systems (page 700). |
| **talkd** | *talk* | Allows you to have a conversation with another user on the same or a remote machine. The **talkd** daemon handles the connections between the machines. The *talk* utility on each system contacts the **talkd** daemon on the other system for a bidirectional conversation. |
| **telnetd** | TELNET | One of the original Internet remote access protocols. |
| **tftp** | TFTP | Used to boot a system or get information from a network. Examples include network computers, routers, and some printers. |
| **timed** | Time server | On a LAN synchronizes time with other computers that are also running **timed**. |

## Proxy Servers

A *proxy* is a network service that is authorized to act for a system while not being part of that system. A proxy server or proxy gateway provides proxy services; it is a transparent intermediary that relays communications back and forth between an application (e.g., a browser) and a server that usually resides outside of a LAN and frequently on the Internet. When more than one process uses the proxy gateway/server, the proxy must keep track of which processes are connecting to which hosts/servers so that it can route the return messages to the proper process. The most commonly encountered proxies are email and Web proxies.

A proxy server/gateway insulates the local computer from all other computers or from specified domains by using at least two IP addresses: one to communicate with the local computer and one to communicate with a server. The proxy server/gateway examines and changes the header information on all packets it handles so it can encode, route, and decode them properly. The difference between a proxy gateway and a proxy server is that the proxy server usually includes cache (page 1241) to store frequently used Web pages so the next request for that page is available locally and quickly; a proxy gateway typically does not use cache. The terms “proxy server” and “proxy gateway” are frequently used interchangeably.

Proxy servers/gateways are available for such common Internet services as HTTP, HTTPS, FTP, SMTP, and SNMP. When an HTTP proxy sends queries from local systems, it presents a single organizationwide IP address (the external IP address of the proxy server/gateway) to all servers. It funnels all user requests to the appropriate servers and keeps track of them. When the responses come back, the HTTP proxy fans them out to the appropriate applications using each machine’s unique IP address, thereby protecting local addresses from remote/specified servers.

Proxy servers/gateways are generally just one part of an overall firewall strategy to prevent intruders from stealing information or damaging an internal network. Other functions, which can be either combined with or kept separate from the proxy server/gateway, include packet filtering, which blocks traffic based on origin and type, and user activity reporting, which helps management learn how the Internet is being used.

## RPC Network Services

Much of the client/server interaction over a network is implemented using the RPC (Remote Procedure Call) protocol, which is implemented as a set of library calls that make network access transparent to the client and server. RPC specifies and interprets messages but does not concern itself with transport protocols; it runs on top of TCP/IP and UDP/IP. Services that use RPC include NFS and NIS. RPC was developed by Sun as ONC RPC (Open Network Computing Remote Procedure Calls) and differs from Microsoft RPC.

- **rpcbind** In the client/server model, a client contacts a server on a specific port (page 312) to avoid any mixup between services, clients, and servers. RPC has two possible ways of registering a port. The first works in the manner of a traditional daemon: The server binds to the port it wants to bind to but then registers with the RPC portmapper daemon (**rpcbind**) on the server. As an example, NFS uses this mechanism to always bind to port 2049. The client’s port is irrelevant most of the time, so it picks a random port.

More commonly, to avoid maintaining a long list of port numbers and to enable new clients/servers to start up without registering a port number with a central registry, when a server that uses RPC starts, it looks in `/etc/rpc` for the service number and then registers itself with **rpcbind** as just described. The **rpcbind** daemon assigns the server a TCP or UDP port number, and the server binds to that port. RPC services typically use service numbers (`/etc/rpc`) that were defined by Sun, but the TCP or UDP port number it uses is random. When a client wants to connect to an RPC server, it first asks **rpcbind** on the server, which listens on port 111, for the name of the service it is interested in (e.g., mountd). If that service is registered, **rpcbind** returns the TCP or UDP port number of the server to the client. The client then contacts the RPC server daemon directly to finish the transaction.

The `/etc/rpc` file (page 510) maps RPC service names to RPC numbers. The `/etc/services` file (page 511) maps system service names to TCP or UDP ports.

The sequence of events for communication between an RPC client and server is as follows:

- 1. The client system needs to talk to a server application running on a remote system. The client system knows which system the server application is running on but not which port it is using. The client system looks for the service name in `/etc/rpc` to determine the service number.
- 2. The client system contacts **rpcbind** on port 111 of the remote system with the service number to ask which UDP or TCP port the server on the remote system is listening on.
- 3. The **rpcbind** daemon on the remote system checks which server applications have registered with it. If the service number the client system asked for is registered, the **rpcbind** daemon on the remote system returns the UDP or TCP port assigned to that server application.
- 4. The RPC libraries on the client system encode procedure calls and send them to the server application on the remote system on the specified port. (The client system issues a "read record from file" request.)
- 5. The server application running on the remote system receives the call, sends it through the RPC libraries to decode it, and generates results. (The filesystem receives the "read record from file" request.)
- 6. The server application passes the results back through the RPC libraries, which encode the results, and then sends the encoded results to the client using the client's registered port. (The read record is returned to the calling program.)
- 7. The client system receives the results, passes them through the RPC libraries for decoding, and presents the decoded results to the user or application that requested them.

If the **rpcbind** daemon stops, you must restart all RPC servers on the local system.
