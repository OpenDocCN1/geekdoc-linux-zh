
## Example:

![](img/477ccb2f05b6ba1b2d563ea74f18c197_569_0.png)

Figure 12-45: The output of the /etc/rpc file.

## The XDR Format

The eXternal Data Representation (XDR) format is a standardized representation of data in the binary format. The XDR format allows systems to communicate across a network, especially across heterogeneous networks. It is developed using the C API programming language. XDR formats are defined in the rpc.h header file. It is primarily used in all Linux- and UNIX-based systems.

## The Portmapper

### Definition:

The portmapper is a program that an RPC application uses to register the port numbers used by the application. This program is stored in the /sbin directory or in the /usr/sbin directory. The portmapper acts as a service agent for all RPC servers running on a system. To access a service with the given program number, the client first queries the portmapper to get information about the port number where the service is available. The portmapper accepts the request, processes it, and returns the TCP and UDP port numbers of the service to the client.

When a system tries to access the portmapper, it reads the hosts.allow and hosts.deny files, which are stored in the /etc directory. These files list the IP addresses of systems to which access is allowed or denied using the portmap variable. The portmapper controls a set of daemons such as nfsd, mountd, ypbind/ypserv, rquotad, lockd, statd, riptime, and users.

> In Linux, the portmapper is referred to as portmap or rpc.portmap.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_570_0.png)

*Figure 12-46: The working of the portmapper program.*

## The portmap Daemon

**Definition:**

*The portmap* service is a daemon that dynamically assigns ports to RPCs for communication between clients and servers. It maps a service name to the port number in which the service is running. It maintains a portmapper that contains a list of ports and the services that are available for access at each port. The portmap program is stored in the /sbin directory. The portmap service can be started only by a superuser.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_570_1.png)

The portmap Daemon

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_571_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_571_1.png)

**Figure 12-47:** The portmap program runs between a server and a client to dynamically assign ports to RPCs.

## NFS Daemons

NFS is implemented by four daemons:

- The **rpc.nfsd** daemon is the primary daemon that handles all NFS requests.
- The **rpc.mountd** daemon evaluates the permissions for an exported filesystem before it is mounted.
- The **rpc.lockd** daemon provides lock recovery on crashed systems.
- The **rpc.statd** daemon handles file locking issues.

## NFS Firewall Options

The portmapper is used to assign ports dynamically to RPC services. This may lead to difficulty when setting up firewalls. Therefore, ports are controlled using the `/etc/sysconfig/nfs` file. By default, the portmapper is assigned to port 111 TCP and UDP, and nfssd is assigned to port 2049 TCP and UDP. The other daemons that are used are mountd, statd, lockd, and rquotad. Variables that are defined in the nfs file are listed in the table. These variables are assigned to a port value that is not being used by any service. While configuring firewalls, all these assigned ports and default ports are allowed to access NFS.

| Variable | Description |
| :--- | :--- |
| MOUNTD_PORT | Specifies the TCP and UDP ports used by the mount service. |
| STATD_PORT | Specifies the status of TCP and UDP ports used by the statd service. |
| LOCKD_TCPORT | Specifies the TCP port used by the lockd service. |

## The Exports File

**Definition:**

The *exports file* is a configuration file that is used to export a filesystem. This file contains definitions, such as the directory to be exported and the clients who can access the directory. Clients are addressed by their hostnames, IP address ranges, IP address or subnet mask combinations, or NIS workgroups. The export options for the client are specified within parentheses, beside the client list. The exports file is stored in the /etc directory. By default, hosts will have read-only access to the filesystem. The exports file can be activated or deactivated using the *exportfs* command.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_572_0.png)

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_572_1.png)

## NFS Shares on the Client-Side

On the client side, NFS shares are mounted using the *mount* command. The syntax of the mount command is: mount *nfs-type* -o *options* remote host:*remote directory local directory*, where *nfs-type* refers to the version of NFS used, *options* refer to the mount options, *remote directory* refers to the location from where the filesystem is to be mounted, and *local directory* refers to the local directory to which the filesystem is to be mounted. During system reboot, the filesystem has to be remounted manually using the mount command.

There are two ways in which the filesystem can be mounted automatically during system reboot.

| Mount Type | Description |
| :--- | :--- |
| /etc/fstab | A line of code is added to the /etc/fstab file that is referenced by the netfs service. NFS shares are mounted when the initialization script runs from the /etc/init.d/netfs file. The syntax of the line that is added is: {server *IP address or host* name} {<u>exported filesystem</u>} {<u>mount point</u>} nfs ({<u>mount options</u>} 0, 0 |
| autofs | It is an automount utility that is used to mount and unmount filesystems automatically without the need for system resources. It compresses kernel modules that implement the filesystems and a user space daemon to control other functions. It uses the /etc/auto.master file as the main configuration file. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_573_0.png)

## The rsync Utility

**Definition:**

The *rsync* utility is a utility that is used to synchronize files among systems. It compares two files and sends only the differences in the compressed form, instead of sending the entire file. The *rsync* daemon is managed using the rsyncd.conf file stored in the /etc directory. The *rsync* utility uses the rsync algorithm to determine differences between files.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_573_1.png)

The syntax of the *rsync* utility is rsync {source file or folder} {destination file or folder}.

## Syntax

## SMBFS and CIFS

The Samba File System (SMBFS) and the Common Internet File System (CIFS) are the standard filesystems that are used in Linux to mount and access shared resources available on a heterogeneous network. SMBFS is used exclusively for Linux systems. CIFS, which is a virtual filesystem, is widely used to share network files and resources. CIFS provides advanced features, such as authentication, Unicode, distributed caching, and other core kernel functions. SMBFS and CIFS can also be construed as client protocols that enable a Linux system, with Samba installed, to act as a server for a network.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_574_0.png)

## Samba Daemons

Samba has three daemons: smbd, nmbd, and winbindd. The smbd and nmbd daemons are controlled by the SMB service and the winbindd daemon is controlled by the WINS service.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_574_1.png)

| Daemon | Description |
| :--- | :--- |
| smbd | The Server Message Block Daemon (smbd) is used for sharing network resources. It is also used to provide user authentication, access control for network resources, and data sharing using the SMB protocol. By default, it listens to the SMB traffic in ports 139 and 445 and is invoked from the /usr/sbin/smbd directory. |
| nmbd | The NetBIOS Name Service Daemon (nmbd) is used to handle WINS requests and resolve NetBIOS names. By default, it listens to the NMB traffic in port 137 and is invoked from the /usr/sbin/nmbd directory. |
| winbindd | The winbindd is used to resolve the user and group information from a Windows NT server in such a way that it is understandable by a UNIX platform. It allows Windows users to access a Unix system using the RPC calls, PAM, and Name Service Switch (NSS). |

## NSS

NSS is a protocol that enables services to access databases to check for user accounts from various sources. This is very useful in situations where one database has to be accessed by multiple services. For example, the hosts database can be accessed by various services, such as NIS and DNS, through NSS.

## The WINS Service

The Windows Internet Naming Service (WINS) is a service that implements the Windows-specific method of name resolution. WINS consists of two main components: the WINS server and the WINS client. WINS translates the IP address on a Windows network to a NetBIOS name. It uses a distributed database that contains the IP addresses and names of the computers on the network. The database is periodically updated with the latest information.
