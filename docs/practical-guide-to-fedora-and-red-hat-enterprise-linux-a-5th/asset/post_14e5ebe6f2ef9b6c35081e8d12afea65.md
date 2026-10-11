
## Table 10-4 Common daemons (continued)

| Daemon | Used for or by | Function |
|---|---|---|
| crond | cron | Used for periodic execution of tasks. This daemon looks in the `/var/spool/cron` directory for files with filenames that correspond to users' usernames. It also looks at the `/etc/crontab` file and at files in the `/etc/cron.d` directory. When a task comes up for execution, **crond** executes it as the user who owns the file that describes the task. |
| dhcpd | DHCP | DHCP client daemon (page 452). |
| dhcpcd | DHCP | Assigns Internet address, subnet mask, default gateway, DNS, and other information to hosts. This protocol answers DHCP requests and, optionally, BOOTP requests. Refer to “DHCP: Configures Hosts” on page 451. |
| ftpd | FTP | Handles FTP requests. Refer to “ftp: Transfers Files over a Network” on page 379. See also **vsftpd** (page 643). Can be launched by **xinetd**. |
| gpm | General-purpose mouse or GNU paste manager | Allows you to use a mouse to cut and paste text on console applications. |
| httpd | HTTP | The Web server daemon (Apache, page 841). |
| in.fingerd | finger | Handles requests for user information from the **finger** utility. Launched by **xinetd**. |
| inetd | | Deprecated in favor of **xinetd**. |
| lpd | Line printer spooler daemon | Launched by **xinetd** when printing requests come to the system. Not used with CUPS. |
| named | DNS | Supports DNS (page 773). |
| nfsd, statd, lockd, mountd, quotad | NFS | These five daemons operate together to handle NFS (page 727) operations. The **nfsd** daemon handles file and directory requests. The **statd** and **lockd** daemons implement network file and record locking. The **mountd** daemon converts filesystem name requests from the mount utility into NFS handles and checks access permissions. If disk quotas are enabled, **quotad** handles those. |
| ntpd | NTP | Synchronizes time on network computers. Requires a /etc/ntp.conf file. For more information go to www.ntp.org. |
| portmap | RPC | Maps incoming requests for RPC service numbers to TCP or UDP port numbers on the local system. Refer to “RPC Network Services” on page 391. |
| pppd | PPP | For a modem, this protocol controls the pseudo-interface represented by the IP connection between the local computer and a remote computer. Refer to “PPP: Point-to-Point Protocol” on page 367. |
| **rexecd** | rexec | Allows a remote user with a valid username and password to run programs on a system. Its use is generally deprecated for security reasons; certain programs, such as PC-based X servers, may still have it as an option. Launched by **xinetd**. |
| **routed** | Routing tables | Manages the routing tables so your system knows where to send messages that are destined for remote networks. If your system does not have a */etc/defaultrouter* file, *routed* is started automatically to listen to incoming routing messages and to advertise outgoing routes to other systems on the local network. A newer daemon, the gateway daemon (*gated*), offers enhanced configurability and support for more routing protocols and is proportionally more complex. |
| **rsyslogd** | System log | Transcribes important system events and stores them in files and/or forwards them to users or another host running the **rsyslogd** daemon. This daemon is configured with */etc/rsyslog.conf* and used with the rsyslog utility. See page 582. |
| **sendmail** | Mail programs | The **sendmail** daemon came from Berkeley UNIX and has been available for a long time. The de facto mail transfer program on the Internet, the **sendmail** daemon always listens on port 25 for incoming mail connections and then calls a local delivery agent, such as */bin/mail*. Mail user agents, such as KMail and Thunderbird, typically use **sendmail** to deliver mail messages. |
| **smbd**, **nmbd** | Samba | Allow Windows PCs to share files and printers with UNIX and Linux computers (page 749). |
| **sshd** | ssh, scp | Enables secure logins between remote systems (page 633). |
| **talkd** | talk | Allows you to have a conversation with another user on the same or a remote machine. The **talkd** daemon handles the connections between the machines. The **talk** utility on each system contacts the **talkd** daemon on the other system for a bidirectional conversation. Launched by **xinetd**. |
| **telnetd** | TELNET | One of the original Internet remote access protocols (page 377). Launched by **xinetd**. |
| **tftp** | TFTP | Used to boot a system or get information from a network. Examples include network computers, routers, and some printers. Launched by **xinetd**. |
| **timed** | Time server | On a LAN synchronizes time with other computers that are also running **timed**. |
| **xinetd** | Internet super-server | Listens for service requests on network connections and starts up the appropriate daemon to respond to any particular request. Because of **xinetd**, a system does not need the daemons running continually to handle various network requests. For more information refer to “The xinetd Super-server” on page 445. |

## Proxy Servers

A *proxy* is a network service that is authorized to act for a system while not being part of that system. A proxy server or proxy gateway provides proxy services; it is a transparent intermediary, relaying communications back and forth between an application, such as a browser and a server, usually outside of a LAN and frequently on the Internet. When more than one process uses the proxy gateway/server, the proxy must keep track of which processes are connecting to which hosts/servers so that it can route the return messages to the proper process. The most commonly encountered proxies are email and Web proxies.

A proxy server/gateway insulates the local computer from other computers or from specified domains by using at least two IP addresses: one to communicate with the local computer and one to communicate with a server. The proxy server/gateway examines and changes the header information on all packets it handles so that it can encode, route, and decode them properly. The difference between a proxy gateway and a proxy server is that the proxy server usually includes *cache* (page 1073) to store frequently used Web pages so that the next request for that page is available locally and quickly; a proxy gateway typically does not use cache. The terms “proxy server” and “proxy gateway” are frequently used interchangeably.

Proxy servers/gateways are available for such common Internet services as HTTP, HTTPS, FTP, SMTP, and SNMP. When an HTTP proxy sends queries from local systems, it presents a single organizationwide IP address (the external IP address of the proxy server/gateway) to all servers. It funnels all user requests to the appropriate servers and keeps track of them. When the responses come back, the HTTP proxy fans them out to the appropriate applications using each machine's unique IP address, thereby protecting local addresses from remote/specified servers.

Proxy servers/gateways are generally just one part of an overall firewall strategy to prevent intruders from stealing information or damaging an internal network. Other functions, which can be either combined with or kept separate from the proxy server/gateway, include packet filtering, which blocks traffic based on origin and type, and user activity reporting, which helps management learn how the Internet is being used.

## RPC Network Services

Much of the client/server interaction over a network is implemented using the RPC (Remote Procedure Call) protocol, which is implemented as a set of library calls that make network access transparent to the client and server. RPC specifies and interprets messages but does not concern itself with transport protocols; it runs on top of TCP/IP and UDP/IP. Services that use RPC include NFS and NIS. RPC was developed by Sun as ONC RPC (Open Network Computing Remote Procedure Calls) and differs from Microsoft RPC.

In the client/server model, a client contacts a server on a specific port (page 387) to avoid any mixup between services, clients, and servers. To avoid maintaining a long list of port numbers and to enable new clients/servers to start up without registering a port number with a central registry, when a server that uses RPC starts, it specifies
