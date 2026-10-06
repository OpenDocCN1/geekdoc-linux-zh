
# Starting and Restarting NFS

To start the NFS server, issue the commands

```
/etc/rc.d/init.portmap start
/etc/rc.d/init.nfs start
```

To restart the NFS server, issue the commands

```
/etc/rc.d/init.portmap restart
/etc/rc.d/init.nfs restart
```

# Stopping the NFS Server

To stop the NFS server, issue the commands

```
/etc/rc.d/init.nfs stop
/etc/rc.d/init.portmap stop
```

# Controlling NFS Server Operation

The exports command lets you control operation of the NFS server on the local host:

- exports -v lists directories and the associated options
- exports -a share exports the specified share
- exports -a exports all shares listed in /etc/exports
- exports -u share unexports the specified share
- exports -ua unexports all shares
- exports -r refreshes the share list

In particular, you should issue the command

```
exports -r
```

after any modification of the /etc/exports file.

# Checking Service Status

To check the status of the NFS server while logged in to the server host, issue the following commands

```
/etc/rc.d/init.nfs status
/etc/rc.d/init.portmap status
```

To check the status of a remote NFS server, issue the command

```
rpcinfo -p server
```

where server is the host name of the NFS server.
To list the shares exported by a server, issue the command

```
showmount -e server
```

where server is the host name of the NFS server.

# Logging

The NFS facility logs messages to the system log file, /var/log/messages.
If NFS is not operating properly, check the system log for messages that point to the source of the problem.
Now take time to complete Exercise 21.5, which gives you experience in working with NFS.

# EXERCISE 21.5

# Installing and Configuring NFS

NFS is an important network service, especially where Unix systems are popular. To gain experience working with NFS, perform these steps:

- 1. Install the NFS server packages on one host and the NFS client packages on another.
- 2. Export the /tmp directory of the NFS server, using default permissions.
- 3. Access the shared directory from the client host and attempt to read a file. The operation should complete successfully.
- 4. Access the shared directory from the client host and attempt to write a file. The operation should fail.
- 5. Revise the share permissions to allow read-write access.
- 6. Access the shared directory from the client host and attempt to write a file. The operation should complete successfully.

You can access this book and the NFS documentation while performing this exercise. But, before taking the RHCE, be sure you can perform such operations as without using books or external documentation.

# Samba

Samba is an open-source implementation of the System Message Block (SMB) service used by Microsoft Windows 9x and NT, which is sometimes known as Common Internet File System (CIFS). Samba is widely used throughout the Unix and Linux communities. Samba originated in the work of Andrew Turnbull, who reverse the SMB protocol. Subsequently, a worldwide team formed to maintain and enhance Samba.

Samba enables Windows clients to access Linux file systems and printers by using the Network Neighborhood facility of the Windows manager. Unix and Linux clients can also access shared file systems and printers. Samba is popular in competing environments that lack Windows clients, because its authentication mechanisms are superior to those of NFS.

SMB is a high-level protocol built on Microsoft's NetBIOS, which can be run over a TCP/IP network. NetBIOS duplicates several TCP/IP functions. For example, it has its own hostname resolution service, Windows Internet Naming Service (WINS).

Samba has two associated services:

- smbd, which authenticates clients, authorizes client access to shares, and provides shared access to files and printers.
- nmbd, which provides a browsing facility that lets clients discover shares and their shares. It also acts as a WINS server, resolving NetBIOS host names to IP addresses.

At any time, one server acts as the browser master for a network served by SMB. The browser master (or master browser, as it's sometimes called) maintains information on available servers and responds to client inquiries attempting to discover servers and shares. Eligible SMB servers compete in an election that determines which becomes the browser master. A Samba server can be configured to participate in such an election or override the election, becoming the browser master despite the presence of other candidate servers.

Linux clients can access SMB shares in two of ways. The smbcclient program provides FTP-like access to shared files and printers, and the smbount command lets you a shared file system such as would a local file system. The standard printtool utility lets you configure access to Samba printers.

# Installation

Samba is contained in three packages:

- samba-common, which contains files needed by Samba clients and servers
- samba, which contains the Samba server
- samba-client, which contains the Samba smclient, smbmount, and smbprint programs and associated files and documentation

Samba is frequently updated; you should consider downloading the latest packages from the Samba Web site, www.samba.org, rather than installing packages contained on Red Hat Linux distribution media.

To install a Samba server, move to the directory containing the packages and issue the command

```
rpm -Uvh samba-*.rpm
```

This command installs both the Samba server and the Samba client.

# Basic Server Configuration

The main configuration file is /etc/smb.conf, which contains two types of directives:

- Global directives
- Service directives

This section explains the contents of /etc/smb.conf. The global section contains the following directives:

# Samba Global Directives

Here are global directives contained in:

```
workgroup = MYGROUP
comment = Router
security = user
map to guest = Bad User
log size = 0
log file = /var/log/samba/%m
socket options = TCP_NODAY
printcap name = /etc/printcap
logon script = %u.bat
domain logons = Yes
os level = 69
preferred master = Yes
domain master = Yes
wins support = Yes
printing = bsd
strict locking = Yes

The hosts allow directive identifies the client hosts permitted to access the server. The local host address, 127.0.0.1, should generally be included in the list of. Several formats are allowed:

- IP address—for example, 192.168.1
- IP address and subnet mask—for example, 192.168.1.0/255.255.255
- Partial IP address—for example, 192.168.1 (not the trailing dot)
- host-name—for example, client.azuspacific.com
- domain or subdomain name—for example, .azuspacific.com
(note the lack of a wildcard and the leading dot)
