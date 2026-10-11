
(DNS, NIS or NIS+), the hosts database is part of the database that the name service assigns for host information. The format of the entries of the hosts database is as follows:

`<IP4 address>  <hostname> <nicknames>  <comment>`

When Solaris first creates the *etc/inet/hosts* file, it contains two entries, one for the loopback and one for the local machine. The loopback address is a private address that lets a local system send messages to itself to test its TCP/IP stack or to communicate with IP services that you don’t want available on your external interfaces. If you had a dual-homed machine, you would see an entry similar to the third line below:

`127.0.0.1  localhost  loghost`  
`192.168.1.1  sunrise #The local system’s host name`  
`192.168.2.1  sunrise2 #This is the interface to the second network for a router`

When you are using a local file for your name service, each system looks into its *etc/inet/hosts* file for the host names and IP addresses of the system on the network. In that case, the *hosts* file must contain at a minimum the loop-back address, the IP address and host name of the local system, the IP addresses and host names of all network interfaces, the IP addresses and host names of hosts and routers on the system, and the IP address of a system that your local system wants to identify by its host name.

**ipnodes database** The ipnodes database contains the IPv6 addresses and host names of systems on your network. For a name service, the ipnodes database is managed as part of the host table in the service.

**netmask database (optional)** The netmask database is used only when your network contains subnets. This database is a list of networks and their associated subnet masks. Subnetting allows you to divide larger networks into smaller networks for administration and performance reasons.

## Dynamic Host Configuration Protocol (DHCP)

Dynamic Host Configuration Protocol (DHCP) is used to automatically supply a TCP/IP address as a service to a system when that system boots up. DHCP servers manage addressing information, provide addresses from a pool, assign a lease or life-time for which a system can maintain a specific address, and provide other services from the DHCP to clients. Properly configured DHCP solves two vexing problems: first, it relieves the rather onerous task of a network administrator having to assign, track, and edit addresses manually in a database or text file, and second, by doling out the addresses to systems as they appear, it helps to alleviate the problem of having limited IP addresses to assign on a network.

Solaris DHCP also offers the additional benefits of supporting BOOTP (BOOTSTRAP Protocol) clients because both BOOTP servers and DHCP servers can listen to and respond to requests from clients using the same messaging structure. DHCP can provide the IP address requested by BOOTP clients. BOOTP can send messages from one network to another. DHCP requests, because they use the same messaging structure, can also be relayed to the router and can't be differentiated from a BOOTP request.

An additional feature that clients obtain from Solaris DHCP is the information needed to have a server boot up on the network. This can take the place of using Reverse Address Resolution Protocol (RARP) and bootparams. DHCP servers supply the IP address, boot server, and network configuration information that a client needs to start up correctly. DHCP is also more efficient at servicing boot requests than other systems because requests can be relayed across subnets.

DHCP is a powerful network function that can save you a lot of time and aggravation if it is set up correctly. Since it is not possible to explain every aspect of DHCP in this publication, it is strongly recommended that you purchase one of the many books that are dedicated solely to the subject of DHCP or link to a Web site such as www.dhcp.org for more comprehensive information.

To start and stop DHCP services on a server, you use the DHCP Manager or a command-line utility. DHCP is typically set up to start up automatically when the server boots, and the service becomes unavailable when the server is shut down. Therefore, DHCP servers are typically left running or backed up with redundant systems.

The DHCP server stores its data in the dhcpdtab file and in a set of DHCP network tables that each has as its file name the number of the network. Thus, a network with the address 192.168.1.1 would store its DHCP information in the table with the name 192_168_1_1.

The DHCP Manager is a GUI utility that you can use on the server to configure, start, stop, disable, and enable the DHCP service. You can also use this tool to customize your DHCP server settings. DHCP lets you choose which IP addresses will be managed, work with network configuration macros, and modify nonstandard network configuration options. You will find a thorough help system provided with the DHCP Manager.

To start the DHCP Manager, do this:

- 1. On a local system, log in as a superuser using the following command:
  ```bash
  # xhost <servername>
  ```
  
  On a remote DHCP server, enter the following:
  
  `# Display=localhost; export display`
  
  `# /usr/sbin/dhcpmgr &`
- 2. Make your changes in the DHCP Manager window.
- 3. Select the Exit command from the File menu.

Here are the four DHCP command-line utilities (each of these four commands is documented in the man pages):

- **in.dhcpd**: This command lets you control the DHCP daemon.
- **dhcpconfig**: This is a shell script that lets you configure the DHCP server using commands presented in a text-based menu system.
- **dhtadm**: This command allows you to change the configuration options and macros for DHCP clients.
- **pntadm**: This command allows you to modify DHCP network tables.

The Solaris DHCP client is the system that accepts the IP address from the server. On Solaris, it is a software program run as a daemon (dhcpagent). Solaris automatically installs the DHCP client as part of the installation of the operating system. You do not need to enable this client because it is already enabled.

## The Network File System

The Network File System (NFS) allows you to work locally with files that are stored on a remote computer disk but appear as if they are present on your own computer. The remote system acts as a file server, and the local system acts as the client and queries the file server.

**NOTE** File systems were covered extensively in Chapter 5. You may want to refer back to that chapter for a more detailed discussion of NFS.

The system administrator configures the NFS just as they do the NIS. If you are working with a file, you will probably not be aware of where the file is physically stored. This is another perfect example of distributed computing. Because most central file servers are equipped with large-capacity disk drives and devices that make backup copies of data, some Solaris systems may be diskless. A floppy disk can be used to start Solaris and load the system software from another machine on the network. Solaris also produces a dataless system that stores only the system software and the operating system, and the applications are kept on the disk.

Use the df utility to display a list of the file systems available on your system (you can use df with the -k option to show it in kilobytes instead of blocks). It will also show you what disk space is free and how much is used. File system names that are prepended with host names are available to you.

All standard Solaris utilities work with NFS remote files in the same way that they operate on files stored locally. The physical location of the files is not important unless you lose access to the files through downtime or temporary unavailability. You will most likely get an error message if the NFS server is not able to respond. It will then give you an OK message when the files become available again.

One of the advantages of distributed computing is that you can log in on any machine on the network and all of your files will be available to you, including your startups scripts. Your home directory will always be available to you on any machine on the network.

## Sharing File Systems

Sharing local files with other machines has many advantages. It saves disk space, which is a major advantage, but it also gives you a single place to change data instead of having to change it several times at different locations. Shared file systems are usually stored under the /export or /usr/export directory (though you can share any file system or directory on your system), and each subdirectory houses a shared file system. Shared files can be kept in any directory.

To share a file system, you must enable NFS by editing /etc/dfs/dfstab. This file is run by the /etc/rc3.d/$15nfs.server script once the system enters run level 3. The syntax is as follows:

```bash
$ cat /etc/dfs/dfstab
# place share (1M) commands here for automatic execution on
#     entering init state 3.

#Issue the command '/etc/init.d/nfs.server start' to run the
#   NFS daemon processes and the share commands, after adding
#   the very first entry to this file.

#Share [-F fstype] [-o options] [-d "<text>"] <pathname>
#  [resource],e.g.,
share -F nfs -o rw-engineering -d "home dirs" /export/home2
share -nfs -o ro-huey, rw=dewey:louie, root=dewey -d 'home \
  directories' /export/home
```
