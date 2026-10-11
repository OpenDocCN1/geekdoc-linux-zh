and reuses it for a while. The nameserver deletes the nonlocal information before it can become outdated. Refer to “TTL” on page 1112.

The system’s translation of symbolic hostnames into addresses is transparent to most users; only the system administrator of a networked system needs to be concerned with the details of name resolution. Systems that use DNS for name resolution are generally capable of communicating with the greatest number of hosts—more than would be practical to maintain in a/etc/hosts file or private NIS database. Chapter 24 covers setting up and running a DNS server.

Three common sources are referenced for hostname resolution: NIS, DNS, and system files (such as /etc/hosts). Linux does not ask you to choose among these sources; rather, the nsswitch.conf file (page 455) allows you to choose any of these sources, in any combination, and in any order.

# PORTS

Ports are logical channels on a network interface and are numbered from 1 to 65,535. Each network connection is uniquely identified by the IP address and port number of each endpoint.

In a system that has many network connections open simultaneously, the use of ports keeps packets (page 1098) flowing to and from the appropriate programs. A program that needs to receive data binds to a port and then uses that port for communication.

Privileged ports Services are associated with specific ports, generally with numbers less than 1024. These ports are called privileged (or reserved) ports. For security reasons, only root can bind to privileged ports. A service run on a privileged port provides assurance that the service is being provided by someone with authority over the system, with the exception that any user on Windows 98 and earlier Windows systems can bind to any port. Commonly used ports include 22 (SSH), 23 (TELNET), 80 (HTTP), 111 (Sun RPC), and 201–208 (AppleTalk).

# NIS: NETWORK INFORMATION SERVICE

NIS (Network Information Service) simplifies the maintenance of frequently used administrative files by keeping them in a central database and having clients contact the database server to retrieve information from the database. Just as DNS addresses the problem of keeping multiple copies of hosts files up-to-date, NIS deals with the issue of keeping system-independent configuration files (such as /etc/passwd) current. Refer to Chapter 21 for coverage of NIS.

# NFS: NETWORK FILESYSTEM

The NFS (Network Filesystem) protocol allows a server to share selected local directory hierarchies with client systems on a heterogeneous network. Files on the remote fileservers appear as if they are present on the local system. NFS is covered in Chapter 22.