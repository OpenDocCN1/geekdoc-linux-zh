
managed by each xdm process. xdm modifies its command-line argument to show the name of the display it is managing. This is an excellent debugging aid.

If a client workstation is having problems connecting to xdm, or dying mysteriously, an error log is written to the xdm's error log file. The location of the error log file is specified in the xdm-config file, which is usually in the /etc/X11/xdm or /etc/X11R6/xdm directory. The default location of the xdm error log file in Red Hat Linux is /var/log/xdm-error.log. Check the contents of the xdm-error.log file for clues. Resource problems, such as not being able to find a font, will also show up in this log file.

If the login process appears to be failing, you can try using the failsafe option. This usually involves pressing the F1 key instead of the Enter key at the time of logging in, after the username and password have been entered. The failsafe option provides a minimal session for debugging. By default a single xterm application is launched for this option.

If none of the X clients are able to get the xdm login prompt, barring network connectivity problems, the problem is almost certainly a dead xdm parent process on the xdm login server. Determine the process ID of the parent xdm process by examining the contents of the /var/run/xdm.pid file. Verify that this process is dead, and start up a new xdm parent process. X clients should now be able to get xdm login windows. You will notice child xdm processes starting up as client workstations start connecting to the xdm login server.

A common problem with the xaccess file is when it contains names of retired hosts whose IP addresses can no longer be resolved. Any valid hostnames that appear after this invalid hostname are not recognized by xdm, and these hosts are unable to receive xdm login windows. The fix is to remove the invalid hostnames from the xaccess file and issue a SIGHUP signal to the parent xdm process.

If everything fails, you can run xdm in debug mode with the -debug command-line option. However this is not very useful from the X Windows System administration point of view. This option is intended for X Windows System developers.

## AUTHENTICATING USERS AND NETWORK RESOURCES

### In this chapter

- Network Authentication in UNIX and Linux 84
- NIS Network Configurations 84
- NIS Maps 86
- Setting Up an NIS Master Server 87
- Setting Up an NIS Client 89
- Adding an NIS Slave Server 91
- Moving NIS Master Functions to Another Machine 91
- Removing an NIS Slave Server 95
- Maintaining NIS Maps 96
- Understanding the Name Server Switch 98
- Useful Scripts 99
- Troubleshooting 101

### Network Authentication in Unix and Linux

Unix and Unix-like operating systems in a networked environment often use a form of centralized user authentication and distribution of resource information (such as user databases or host tables).

Often, these services are provided using the Network Information Service (NIS). NIS was originally designed by Sun Microsystems and was formerly known as Yellow Pages, a name that turned out to be a registered trademark owned by British Telecom. As a result, the name was changed to NIS.

The purpose of NIS is to place network information in a centralized database that can be used by any machine on the network. The following is the information most commonly distributed with NIS:

- hosts maps (`/etc/hosts`)
- passwd maps (`/etc/passwd`)
- group maps (`/etc/group`)
- netgroup maps (`/etc/netgroup`)
- services maps (`/etc/services`)

By running NIS, system administration demands can be eased. For instance, changing a password entry in the NIS database reflects the change to all systems on the network running NIS client programs. There is no need to maintain individual password entries on each machine on the network and make changes to all these databases each time a password changes.

NIS operates using a client/server architecture. NIS databases are replicated across one or more servers. Generally, a network will have one NIS master server along with one or more optional NIS slave servers. The master server holds the read-write NIS database. Read-only copies of this database are replicated to slave servers. The slave servers provide load balancing and answer client broadcast queries. Changes to database contents are made on the master server.

### NIS Network Configurations

The simplest NIS network configuration is to create a network with a master NIS server and one or more NIS client systems, as illustrated in Figure 6.1.

However, most networks are more complicated than this simple example. For instance, on a larger network that requires high-availability, having slave servers can be a good idea. These servers not only help minimize the load on any one NIS server, thus improving responsiveness, but they also provide redundancy so that if one NIS server is not functioning, another can answer requests for NIS services.

**Figure 6.1**  
A simple NIS network with a single NIS master server.

![](img/6c13bcf02a08ad7923caab46f051d96a_103_0.png)

A typical network with an NIS master server and two slave servers is shown in Figure 6.2.

**Figure 6.2**  
An NIS network with a single NIS master server and two slave servers.

![](img/6c13bcf02a08ad7923caab46f051d96a_103_1.png)

### ROUTED NETWORK

Both examples of simple single and multiple NIS server networks shown previously have one thing in common: All the client and server machines are on the same single network. However, the typical corporate network will have more than one network connected through routers. These separate physical networks may reflect geographic distribution of the organization or simply workgroup distinctions.

Often on these networks, the same user database needs to be accessible throughout all the organization’s networks. However, NIS uses broadcasting for the client systems to find a server to service requests. Because an NIS master server can only exist on one physical network, slave servers are needed to play the role of duplicating the NIS databases on each physical network and answering requests for service on those networks.

In Figure 6.3, the entire organizational infrastructure consists of two physical networks connected by a router. The NIS master server is on network A. However, NIS clients on network B won’t be able to find the master server because their broadcast requests searching for the server won’t cross the router. By placing a slave server on network B, the clients on network B will talk to the slave server to service all their NIS requests. The slave and master servers then communicate across the router for the purpose of synchronizing changes from the master NIS server to the slave.

> **Note**  
> While NIS clients often broadcast to find a server to handle their requests, you can configure an NIS client to use a specific host as its NIS server. In this case, an NIS client can communicate with an NIS server across a router because the hostname and IP address of the server are hard-coded in the client's configuration. In this case, the name and IP address of the NIS server needs to be contained in the `/etc/hosts` file on the client system.

**Figure 6.3**  
A routed network configuration with master and slave NIS servers on separate physical networks.

![](img/6c13bcf02a08ad7923caab46f051d96a_104_0.png)

### NIS MAPS

NIS was designed to provide a centralized location for a large number of standard Unix configuration files, generally stored in the `/etc` directory. As a result, NIS has available a large number of tables, known as *maps*, as outlined in Table 6.1.

**Table 6.1 — NIS Maps**

| Map Name | Description |
|---|---|
| `bootparams` | Lists diskless clients and location of files needed for booting |
| `ethers.byaddr` | Lists the Ethernet addresses of hosts and their corresponding names |
| `ethers.byname` | Lists names of hosts and their corresponding Ethernet addresses |
| `groups.bygid` | Lists membership information about groups using group id as the key |
| `groups.byname` | Lists membership information about groups using group name as the key |
| `hosts.byaddr` | Lists names and IP address of hosts using IP addresses as the key |
| `hosts.byname` | Lists names and IP addresses of hosts using hostnames as the key |
| `mailaliases` | Lists all mail aliases |
