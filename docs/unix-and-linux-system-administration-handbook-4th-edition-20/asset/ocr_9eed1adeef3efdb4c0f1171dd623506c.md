# How services are filtered

Although these tools are capable of sophisticated filtering and bring a extra dose of security, we generally discourage the use of UNIX and Linux systems as network routers, and most especially, enterprise firewall routers. The complexity of general-purpose operating systems makes them inherently less secure and less reliable than task-specific devices. Dedicated appliances such as those made by Check Point and Cisco are a better option for site-wide protection.

# How services are filtered

Most well-known services are associated with a network port in the /etc/services or its vendor-specific equivalent. The daemons that provide these services bind to the appropriate ports and wait for connections from remote sites. Most of the well-known service ports are “privileged,” meaning that their port numbers are in the range 1 to 1023. These ports can only be used by a process running as root. Port numbers 1024 and higher are referred to as unprivileged ports.

Service-specific filtering is based on the assumption that the client (the machine that initiates a TCP or UDP conversation) uses an unprivileged port to the server. For example, if you wanted to only allow inbound SMTP connections to a machine with the address 192.108.21.200, you would install a filter that allowed TCP packets destined for port 25 at that address and the exact way that such a filter installed depends on the kind of router or filtering system you are using.

Some services, such as FTP, add a twist to the puzzle. The FTP protocol actually uses two TCP connections when transferring a file: one for commands and the other for data. The client initiates the command connection, and the server initiates the data connection. Ergo, if you want to use FTP to retrieve files from the Internet, you must permit inbound to all unprivileged TCP ports since you have no idea what port might use to form an incoming data connection.

This largely defeats the purpose of packet filtering because some notoriously insecure services (for example, X11 at port 6000) naturally binds to unprivileged ports. This configuration creates an opportunity for curious users within your organization to start their own services (such as a telner server at a nonstandard and unprivileged port) that they or their friends can access from the Internet.

One common solution to the FTP problem is to use the SSH file transfer protocol. The protocol is currently an Internet draft but is widely used and mature. It is commonly used as a subcomponent of SSH, which provides its authentication and

+   In many cases, inetd or xinet does the actual waiting on their behalf. See page 1188 for details.
Port 25 is the SMTP port as defined in /etc/services.
This summary describes traditional FTP, also known as “active FTP.” Some systems support “passive FTP,” in which the client initiates connections.

![](bbox=[0.95, 0.343, 0.99, 0.433])