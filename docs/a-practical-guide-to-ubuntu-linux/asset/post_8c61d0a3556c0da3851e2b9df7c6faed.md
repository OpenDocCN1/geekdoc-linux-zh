
## INTRODUCTION TO NIS

A primary goal of a LAN administrator is to make the network transparent to users. One aspect of this transparency is presenting users with similar environments, including usernames and passwords, when they log in on different machines. From the administrator's perspective, the information that supports a user's environment should not be replicated but rather be kept in a central location and distributed as required. NIS simplifies this task.

As with DNS, users need to be aware that NIS is managing system files. Setting up and maintaining NIS databases are tasks for the system administrator; individual users and users on single-user Linux systems rarely need to work directly with NIS.

NIS used to be called the Yellow Pages, and some people still refer to it by this name. Sun renamed the service because another corporation holds the trademark to the Yellow Pages. The names of NIS utilities and files, however, are reminiscent of the old name: ypcat displays and ypmatch search NIS files, and the daemon is named ypserv.

## How NIS Works

- NIS does not encrypt data that it transfers over the network—it transfers data as plain text.
- NIS makes a common set of information available to systems on a network, referred to as an NIS domain, is characterized by each system having the same NIS domain name (different than a DNS domain [page 1146]). Technically an NIS domain is a set of NIS maps (database files).
- Each NIS domain must have exactly one master server; large networks may have slave servers. Each slave server holds a copy of the NIS database from the master. The need for slave servers is based on the size of the NIS domain and the reliability of the systems and network. A system can belong to only one NIS domain at a time.
- Whether a system uses NIS, DNS, local files, or a combination of these as the source of information, and in what order, is determined by /etc/nwitch.conf file (page 475). When it needs information from the NIS database, a client requests the information from the NIS server. For example, when a user attempts to log in, the client system must authenticate the user with username and password information from the NIS server.

You can configure nswitch.conf to cause etc/passwd override NIS password information for the local system. When you do not export the root account to NIS (and you should not), this setup allows you to have a unique root password (or no root password, if the root account is locked) for each system.

Under Ubuntu Linux, NIS retrieves the information it offers—such as usernames, passwords, and system names and IP addresses—from local ASCII configuration files such as /etc/passwd and /etc/hosts. These files are called source files or master files. (Some administrators avoid confusion by using different files to hold local configuration information and NIS source information.) An NIS server can include information from as many of the following source files as is appropriate:

- /etc/group Defines groups and their members
- /etc/gshadow Provides shadow passwords for groups
- /etc/hosts Maps local systems and IP addresses
- /etc/passwd Lists user information
- /etc/printcap Lists printer information
- /etc/rpc Maps RPC program names and users
- /etc/services Maps system service names and port numbers
- /etc/shadow Provides shadow passwords for users

The information that NIS offers based on files that change from time to time. NIS is responsible for making the updated information available in a timely manner to all systems in the NIS domain.

Before NIS can store the information contained in a source file, it must be converted to a dbm (page 1144) format called a map. Each map is indexed on one field (column). Records (rows) from a map can be retrieved by specifying a value for the indexed field. Some files generate two maps, each indexed on a different field. For example, the /etc/passwd file generates two maps: one by username, the other indexed by UID. These maps are named passwd.byname and passwd.uid, respectively.

NIS maps correspond to C library functions. The getpwname() and getpuid() obtain username and UID information from /etc/passwd on non-NIS systems. On NIS systems, these functions place RPC to the NIS server in a process that is transparent to the application function.

The names of the NIS maps correspond to the files in the /var/yp/nisdomain-directory on the master server, where nisdomain is the name of the NIS domain. In the examples in this chapter the NIS domain is named:

```bash
$ ls /var/yp/maps
group.bygid netgroup.byname protocols.byname services.byservice
group.byname netgroup.passwd protocols.number shadow.byname
hosts.byaddr netid.byname rpc.rpc
hosts.byname passwd.byname rpc.number ypersvers
netgroup passwd.byname services.byname
```

To recall NIS maps, you can assign nicknames to them. The /var/yp/nicknames file on both clients and servers holds a list of commonly used nicknames:

```bash
$ cat /var/yp/nicknames
passwd passwd.byname
group group.byname
networks networks.byaddr
hosts hosts.byname
protocols protocols.number
services services.byname
aliases mail.aliases
ethers ethers.byname
```

You can also use the command ypcat -x to display the list of nicknames. Each line in nicknames contains a nickname followed by whitespace and the name of the map corresponding to the nickname. You can add, remove, or modify nicknames by changing the nicknames file.

Displaying maps The ypcat and ypmatch utilities display information from the NIS maps on the server. Using the nickname password, the following command, which you can run on any server, shows:

```bash
$ ypcat -x
passwd passwd.byname
group group.byname
networks networks.byaddr
hosts hosts.byname
protocols protocols.number
services services.byname
aliases mail.aliases
ethers ethers.byname
```

## INTRODUCTION TO NIS 743

## Running an NIS Client

This section explains how to set up an NIS client on the local system.

### PREQUISITES

Install the following packages:

- nis
- portmap (installs automatically with nis)

When you install the nis package, the dpkg postinst script starts an NIS client. The "nis init script" section below is if you want to start an NIS server or do not want to start a client. The dpkg postinst script asks you to specify the NIS domain name of the local system if it does not find one in /etc/default/nis. If necessary, the script creates this file and stores the domain name in it. If file does not exist, the NIS client (ypbind) will not start. If there is a server for the domain you specify, the client quickly binds to that server.

If there is no server for the client to bind to when you install or start NIS client, the client spends several minutes trying to find a server, displaying the following message while so:

```
- Setting up (3.17-14ubuntu2) ...
- Setting NIS hostname to: 
- Starting NIS services
- binding to YP server...
- *
-*
```

Finally the client (ypbind) gives up on finding a server and runs in the background in broadcast mode:

```bash
$ ps -ef grep ypbind
root      16832 1 0 19:33 7      00:00:00 /usr/sbin/ypbind -broadcast
sam       17390 5839 0 19:38 pts/0      00:00:00 grep ypbind
```

Broadcast mode is less secure than other modes because it exposes the system to rogue servers by broadcasting a request for a server to identify itself. If ypbind starts in this mode, it is a good idea to set up an NIS server (page 750) and configure an NIS client as explained in the next section.

After you configure, call the nis init script to restart nis. However, as explained earlier, starting nis takes a while if it cannot connect to a server. The /etc/default/nis file specifies which script starts an NIS client, or both:

```bash
$ sudo service nis restart
```

After changing the nis configuration on an active server, reload in place of restart to reload configuration files without disturbing clients to the server.

## NOTES

If there is no NIS server for the local system's NIS domain, you need to set up one (page 750). If there is an NIS server, you need to know the name of the NIS domain
