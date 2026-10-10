
# Query Portmapper for RPC Services

The Portmapper server can be queried for the RPC services registered with it by using the `rpcinfo` tool:

```bash
rpcinfo -p hostname
```

For example:

```bash
(bash)$ rpcinfo -p 192.168.1.1
   program vers proto  port
   100000   4    tcp   111  portmapper
   100000   3    tcp   111  portmapper
   100000   2    tcp   111  portmapper
   100000   4    udp   111  portmapper
   100000   3    udp   111  portmapper
   100000   2    udp   111  portmapper
   100024   1    udp 32782  status
   100024   1    tcp 32779  status
   100133   1    udp 32782
   100133   1    tcp 32779
   100021   1    udp 4045  nlockmgr
   100021   2    udp 4045  nlockmgr
   100021   3    udp 4045  nlockmgr
   100021   4    udp 4045  nlockmgr
   100021   1    tcp 4045  nlockmgr
   100021   2    tcp 4045  nlockmgr
   100021   3    tcp 4045  nlockmgr
   100021   4    tcp 4045  nlockmgr
   100005   1    udp 32795  mountd
   100005   2    udp 32795  mountd
   100005   3    udp 32795  mountd
   100005   1    tcp 32784  mountd
   100005   2    tcp 32784  mountd
   100005   3    tcp 32784  mountd
   100003   2    udp 2049  nfs
   100003   3    udp 2049  nfs
   100227   2    udp 2049  nfs_acl
   100227   3    udp 2049  nfs_acl
   100003   2    tcp 2049  nfs
   100003   3    tcp 2049  nfs
   100227   2    tcp 2049  nfs_acl
   100227   3    tcp 2049  nfs_acl
   100011   1    udp 51802  rquotad
   100235   1    tcp 55451
   100004   2    udp 1007  ypserv
   100004   1    udp 1007  ypserv
   100004      1   tcp       762    ypserv
   100004      2   tcp      51059   ypserv
   100007      3   udp      56186   ypbind
   100007      2   udp      56186   ypbind
   100007      1   udp      56186   ypbind
   100007      3   tcp      51390   ypbind
   100007      2   tcp      51390   ypbind
   100007      1   tcp      51390   ypbind
```

# Chapter 3: Enumeration

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_101_0.png)

The `rpc.rusersd` and `rpc.who` services are two RPC services that provide user information similar to finger:

```bash
[bash]$ rusers -l 192.168.1.1
bob   192.168.1.1:pts/1 Jan 15 14:26 :08 (bob@ispaddress.bobhisp.org)
rob   192.168.1.1:pts/4 Jan 15 13:10 1:04 (dhcp.rob@homeisp.org)
```

```bash
[bash]$ rwho 10.0.0.1
deepi 10.0.0.10:pts/2   Jan 15 10:10
joe   192.168.1.11:pts/1  Jan 12 14:33
```

## Disable Portmapper and RPC Services

If you are running any RPC services, the following suggestions are strongly recommended:

-   Disable Portmapper if no RPC services are running.
-   Disable `rpc.rusersd` and `rpc.who` by commenting out the appropriate line(s) in `inetd.conf`. If using `xinetd`, look in your `xinetd.d` directory and make sure the files corresponding to the services you want to disable contain this line: `disable = yes`.
-   Disable any RPC services that are not in use.

You must restart `inetd` or `xinetd` in order for changes to take effect.

## NNTP (Network News Transfer Protocol): 119 (TCP)

NNTP is a protocol for the distribution, inquiry, retrieval, and posting of news articles.

### Obtain the NNTP Server Banner

Many NNTP servers will print out version information when connected to:

```bash
[bash]$ telnet 192.168.1.1 119
Connected to 192.168.1.1.
Escape character is '^]'.
200 192.168.1.1 InterNetNews NNTP server INN 1.4 22-Dec-93
ready (posting ok).
```

### Change the NNTP Server Banner

Many NNTP servers require their source code to be edited in order to change the server banner. In these cases, you must obtain the source code to your NNTP server and search for the version string by using the `grep` command. Once you have edited the source code to reflect the new banner information, recompile and reinstall the NNTP server. Some NNTP servers allow for banner information to be changed by editing appropriate configuration files. Please see your NNTP server documentation for details.

## Samba: 137 to 139 (TCP and UDP)

Samba uses the SMB (Server Message Block) protocol to share files and printers over the network. SMB is most commonly used by Microsoft Windows operating systems. See [http://www.samba.org](http://www.samba.org) for details on the Samba project.

### Enumerate Samba Server Information

Samba's `smbclient` tool can be used to enumerate information from a remote Samba server:

```bash
[bash]$ smbclient -L sambsserver -I 10.0.0.1 -U ''
added interface ip=192.168.1.2 bcast=192.168.1.255 nmask=255.255.255.0
Password: [enter]
Domain=[REMOTEDOMAIN]  OS=[Unix]  Server=[Samba 2.2.8]

Sharename       Type      Comment
---------       -----     -------
IPC$            IPC       IPC Service (Samba Server)
ADMIN           Disk      IPC Service (Samba Server)

Server          Comment
--------        -------
SAMBEASERVER

Workgroup       Master
---------       ------
RGROUP          RMASTERHOST
```

### Change the Samba Server String and Version Information

The following steps can be taken to harden Samba server configurations:

-   Edit `smb.conf` and change `server string = Samba Server` to something else: `server string = no information`. This will change the description field displayed next to each share name.
-   Also, make use of the `hosts allow` and `interfaces` settings in `smb.conf` in order to restrict external hosts from connecting to your Samba server.
-   In order to change the actual Samba version information, edit the `source/include/version.h` file and change the value of the constant `VERSION` to something else. You must recompile and reinstall Samba for the change to take effect.

## IMAP2/IMAP4 (Internet Message Access Protocol 2/4): 143 (TCP)

IMAP2/4 is an e-mail access protocol used to access e-mail from a mailbox server. Its features include the ability to store e-mail on a remote location.

### Grab the IMAP Server Banner

IMAP2/4 servers are known to print out a welcome banner with version information when connected to:

```bash
[bash]$ telnet 192.168.1.1 143
Connected to 192.168.1.1.
Escape character is '^]'.
* OK 192.168.1.1 IMAProver1 v12.264 server ready
```

### Change the IMAP Server Banner

Many IMAP servers require their source code to be edited in order to change the server banner. In these cases, you must obtain the source code to your IMAP server and search for the version string by using the `grep` command. Once you have edited the source code to reflect the new banner information, recompile and reinstall the IMAP server. Some IMAP servers allow for banner information to be changed by editing appropriate configuration files. Please see your IMAP server documentation for details.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_103_0.png)

## SNMP (Simple Network Management Protocol): 161, 162 (UDP)

SNMP is a maintenance protocol used to manage nodes such as routers and switches on an IP network.

### Enumerate SNMP

SNMP servers are configured with a “community string” that acts like a user id or password. When an SNMP server is queried with the wrong community string, it does not respond. Many SNMP servers have default community strings such as “public” and “private.” When an SNMP server is queried with the right community string, useful information can be gained:

```bash
[bash]$ snmpwalk 10.0.0.1 public
TCP/IP
system.sysObjectID.0 = OID: enterprise.36.2.15.2.3
system.sysUpTime.0 = Timeticks: (190724809) 22 days, 1:47:28:09
system.sysContact.0 = unknown
system.sysName.0 = 10.0.0.1
system.sysLocation.0 = Room G11, Ground Floor
interfaces.ifTable.ifEntry.ifPhysAddress.1 = 0:0e7:1:e3:1
interfaces.ifTable.ifEntry.ifPhysAddress.2 =
interfaces.ifTable.ifEntry.ifPhysAddress.3 =
interfaces.ifTable.ifEntry.ifPhysAddress.4 =
```

The preceding output is only a snippet of an output that is usually few hundred lines long. As is obvious, the preceding information provides a lot of configuration details. The `snmpwalk` command is part of the `net-snmp-utils` package provided by most Unix and Linux distribution vendors. It can also be obtained from [http://www.net-snmp.org/](http://www.net-snmp.org/).

### Prevent SNMP Enumeration

If you have any hosts configured to use SNMP, do consider the following precautions:

-   Use SNMP versions 2 or 3.
-   Use a community string that is hard to guess.
