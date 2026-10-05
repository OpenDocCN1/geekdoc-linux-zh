
# 400 CHAPTER 10 NETWORKING AND THE INTERNET

| gov | com | edu | mil | org | net |
| :--- | :--- | :--- | :--- | :--- | :--- |
| example | berkeley | | | moma | |
| bravo | kudos | okeffe | | | okeffe |

**Figure 10-3** U.S. top-level domains

Unlike addresses, domain names were once assigned by the Network Information Center (NIC); now they are assigned by several companies. A system's full name, referred to as its *fully qualified domain name (FQDN), is unambiguous in the way that a simple hostname cannot be. **okeffe.berkeley.edu** at the University of California at Berkeley (Figure 10-3) is not the same as one **okeffe.moma.org**, which might represent a host at the Museum of Modern Art. The domain name not only tells something about where the system is located but also adds diversity to the namespace to avoid confusion when different sites choose similar names for their systems.

Unlike the filesystem, the top-level domain names are last (not case sensitive, so the names okeffe.berkeley.edu, okeffe.Berkeley.edu, and okeffe.Berkeley.edu refer to the same computer. When a domain has been assigned, the local site is free to extend the hierarchy to meet local needs.

With DNS, email addressed to **user@example.com** can be delivered to the computer name **example.com** that handles the corporate mail and knows how to forward messages to mailboxes on individual machines. As the company grows, its site administrator might decide to create organizational or geographical subdomains. The name **delta.example.com** might refer to a system that supports California offices, for example, where **alpha.example.com** is designated to Colorado. Functional subdomains could be another choice, with **delta.sales.example.com** and **alpha.dev.example.com** representing the sales and development divisions, respectively.

BIND On Linux systems, the most common interface to the DNS is BIND (Berkeley Internet Domain Name). BIND follows the client/server model. If one or more systems are running a nameserver, supporting all the local hosts as clients. When it wants to send a message to another host, a system queries the nearest nameserver to learn the remote host's IP address. The client, called *resolver*, may be a process running on the same computer as the nameserver, or may pass the request over the network to a server. To reduce network traffic and facilitate name lookups, the local nameserver maintains some knowledge of distant hosts. If the local server must contact a remote server to pick up an address, when the answer comes back, the local server adds that address to its internal table and reuses it for a while. The nameservers deletes the nonlocal information before it can become outdated. Refer to “TTL” on page 1178.

The system's translation of symbolic hostnames to addresses is transparent to most users; only the system administrator of a networked system needs to be concerned with the details of name resolution. Systems that use DNS for name resolution are generally capable of communicating with the greatest number of hosts—more than would be practical to maintain in a /etc/hosts file or private NIS database. Chapter 24 covers setting up and running a DNS server.

Three common sources are referenced for hostname resolution: NIS, DNS, and system files (such as /etc/hosts). Linux does not ask you to choose among these sources; the nsswitch.conf file (page 475) allows you to choose any of these sources, in any combination, and in any order.

# PORTS

Ports are logical channels on a network interface and are numbered from 1 to 65,533. Each network connection is uniquely identified by the IP address and port number of endpoint.

In a system that has many networks open simultaneously, the use of ports keeps packets (page 1164) flowing to and from the appropriate programs. A program that needs to receive data binds to a port and then uses that port for communication.

Privileged ports Services are associated with specific ports, with numbers less than 1024. These ports are called privileged (or reserved) ports. For security reasons, only a process with root privileges can bind to privileged ports. A service run on a privileged port provides assurance that the service is being provided by someone with authority over the system, with the exception that any user on Windows 98 and earlier Windows systems can bind to any port. Commonly used ports include 22 (SSH), 23 (TELNET), 80 (HTTP), 111 (Sun RPC), and 201–208 (AppleTalk).

# NIS: NETWORK INFORMATION SERVICE

NIS (Network Information Service) simplifies the frequently used administrative files by keeping them in a central database and having clients the database server to retrieve information from the database. As DNS addresses the problem of keeping multiple copies of hosts up-to-date, NIS deals with the issue of keeping system-independent configuration files (such as /etc/passwd) current. Refer to Chapter 21 for coverage of NIS.

# NFS: NETWORK INFORMATION SYSTEM

The NFS (Network Filesystem) protocol allows a server to share local directory hierarchies with client systems on a heterogeneous network. Files on the remote fileserver appear as if they are present on the local system. NFS is covered in Chapter 22.

# NETWORK SERVICES

Linux Internet services are provided by daemons that run continuously or by a daemon that is started automatically by the inet or xinet daemon (page 464) when a service request comes in. The /etc/services files list network services (for example, telnet, ftp, and ssh) and their associated numbers. Any service that uses TCP/IP or UDP/IP has an entry in it. IANA (Internet Assigned Numbers Authority) maintains a database of all permanent, registered services. The /etc/services file lists a small, commonly used subset of services.

Most of the daemons (the executable files) are stored in /usr/bin. By convention, the names of daemons end with the letter d to distinguish them from utilities (one common daemon whose name does not end in d is sendmail). The prefix in- or rpc is often used for daemon names. Refer to “The Upstart Event-Based init Daemon” on page 432 and “SysInit (rc) Start and Stop System Services” on page 440 for information about starting and stopping these daemons.

To see how a daemon works, consider what happens when you run ssh. The local system contacts the ssh (sshd) on the remote system to establish a connection. The two systems negotiate the connection according a a fixed protocol. Each system identifies itself to the other, and then they take turns asking each other specific queries and waiting for valid replies. Each network service follows its own protocol.

# COMMON DAEMONS

In addition to the daemons that support the utilities described up to this point, many other daemons support system-level services that you will interact with. Table 10-4 lists some of these daemons.

| Table 10-4 Common daemons |
| Daemon | Used for | Function |
| :--- | :--- | :--- |
| acpid | Advanced configuration and power interface | Reports and takes action on specified changes in system power, including shutdowns. Useful with machines, such as laptops, that run on batteries. |
| anacron | anacab | Used for periodic execution of tasks. This daemon looks in /etc/anacab file. When a task comes for execution, anacron executes it the user who owns the file. |
| atd | at | Executes a command once at a specific time and date. |
 automount | | mounting | Automatically mounts filesystems when they are accessed. Automatic mounting is a way of demand-mounting remote directories without having to hard-code them into /etc/fstab. See page 792. |
| cron | crontab | Used for periodic execution of tasks. This daemon looks in /var/spool/cron/crontabs directory for filenames that correspond to users' usernames. It also looks at the /etc/crond directory. When a task comes up for execution, cron executes it the user who owns the file. |
| dhcpd | DHCP | Assigns Internet address, subnet mask, default gateway, DNS, and other information to hosts. This protocol answers DHCP requests and, optionally, BOOTP. Refer to "DHCP: Configure Network Interfaces" on page 470. |
| exim4 | Mail programs | The exim4 daemon of the University of Cambridge. The exim4 daemon listens on port 25 for incoming mail connections and then calls a local delivery agent, such as /bin/mail. Mail agents (MUAs), such as KMail and Thunderbird, typically use exim4 to deliver messages. |
| ftpd | FTP | Handles FTP requests. Refer to "ftp: Transfers Files over a Network" on page 393. See also vsftpd (page 687). |
| gpm | General-purpose mouse or GNU paste manager | Allows you to use a mouse and paste to console applications. |
| in.fingerd | finger | Handles requests for user information from the finger utility. |
| inetd | | Listens for service requests on network connections and starts the appropriate daemon to respond to any particular request. Because of inetd, a system does not need the daemons running continuously to handle various network requests. For more information refer to page 464. Deprecated in favor of xinetd. |
| lp | Line printer spooler daemon | Launched by xinetd when printing requests come to the machine. Not used with CUPS. |
