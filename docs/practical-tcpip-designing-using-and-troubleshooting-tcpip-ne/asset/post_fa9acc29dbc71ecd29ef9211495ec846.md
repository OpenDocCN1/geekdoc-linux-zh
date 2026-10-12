
See the Notes in Chapter 18 for general references on Microsoft Windows Networking. RFC-1001 in particular gives an excellent and readable explanation of how NetBIOS name resolution works using broadcasts and also using a WINS-like name server. The *Resource Kit Networking Guide* is also good, but takes too much for granted. The Samba documents give good insights into name resolution, in particular:

- * [NetBIOS.txt](#) *Definition of NetBIOS Protocol and Name Resolution Modes in the Samba distribution* or at
- http://www.samba.org/samba/ftp/docs/textdocs/NetBIOS.txt

We’ve ignored NetBIOS *scope* completely. It’s a way to have separate NetBIOS “universes” on the same wire; machines with one NetBIOS scope can’t communicate (and can’t even “see”) machines with a different scope. Microsoft recommend that you don’t use it.

The resource kit contains three useful tools. We already mentioned *winsdmp* and *winscl* in Module 19.5. The third is *winschk*, which checks out your WINS configuration. It lets you verify that specified names are in specific WINS databases, check that your WINS replication configuration is OK, and continually monitor for WINS replication communications failures.

### NetBIOS name types

- MS-KB-Q119495 *List of Names Registered with WINS Service*
- MS-KB-Q314104 *A List of Names That Are Registered by Windows Internet Naming Service*

The following is a much longer list:

- MS-KB-Q163409 *NetBIOS Suffixes (16th Character of the NetBIOS Name)*

For an explanation of “normal group” versus “Internet group,” see:

- MS-KB-Q140064 *WINS Static Entry Descriptions*
- WINS Manager Help, search for *Using Type Options* and view the link *Internet Group Type*

We have concentrated on computer and domain names in this chapter, but usernames are also registered in NetBIOS, as *username<03>*. This lets Windows send a message or alert to a particular user very easily. *username<03>* resolves to the IP number of the computer that *username* is logged onto, so Windows can send the message directly to that computer. Windows doesn’t have to do an exhaustive search of each machine to see if the user is logged on there.

### WINS architecture and implementation

Microsoft’s white paper on WINS is very readable and informative:

- ftp://ftp.microsoft.com/bussys/winnt/winnt-docs/papers/winswp.doc

For information about running multiple WINS servers, how to estimate the load, and decide on the number and location of servers, and configuring database replication between them:

- Resource Kit, Chapter 8

### WINS client configuration

- MS-KB-Q150737 Setting Primary and Secondary WINS Server Options
- MS-KB-Q173525 WINS Client May Switch Primary and Secondary WINS Servers

Multi-homed (i.e. with more than one IP address) WINS server can cause problems:

- MS-KB-Q185786 Recommended Practices for WINS

The following article describes a problem you can have with WINS, although it’s also interesting for the insight it gives on how WINS systems replicate:

- MS-KB-Q168076 WINS Fails to Converge

### WINS proxy agent

- MS-KB-Q121004 WINS Proxy Agent Functionality
- MS-KB-Q164765 How to Enable WINS Proxy Agent in Windows NT 4.0
- ftp://ftp.microsoft.com/bussys/winnt/winnt-docs/papers/tcpimp2.exe Microsoft Windows NT 3.5/3.51/4.0: TCP/IP Implementation Details. TCP/IP Protocol Stack and Services, Version 2.0

### WINS database replication – “tombstoning” and “scavenging”

In Module 19.6 we explained that if you have multiple WINS servers, they replicate entries from one to another. You can explicitly delete an entry for a name on a WINS server, using WINS Manager (below). However, if the entry had previously been replicated to other servers, the entries on those servers will not be deleted. Worse, those servers may replicate back to this server the entry you just deleted. To avoid this, instead of “deleting” the entry, you **tombstone** it. This marks it as extinct, so the server will never use the entry to reply to a NetBIOS name query from a client. However, the entry is not physically removed, but can be replicated in its tombstoned state to other servers, which in turn mark it as extinct. This prevents the deleted entry being replicated back to the original server and ensures that the entry is eventually marked as extinct on every WINS server on the network. When you attempt to remove an entry, WINS Manager will ask you whether you want to perform a simple delete or a tombstone.

![](img/a2132b646d336d5f9a21102d6320e537_550_0.png)

The WINS server automatically **scavenges** its database periodically, to physically remove extinct items that have been replicated across the whole network, so preventing the database growing forever.

### NetBIOS name cache

- MS-KB-Q236901 NetBIOS Remote Name Cache Time-Out Is 60 Seconds Off

### LMHOSTS file

Using Lmhosts is not resilient:

- MS-KB-Q163949 Workstation Using LMHosts Fails to Logon if Domain Controller Unavailable

See also the references for Lmhosts in the Notes for Chapter 20.

### Node type and name resolution order

- MS-KB-Q160177 Default Node Type for Microsoft Clients

For a (relatively unlikely) example of when you might use an M-node type, see:

- MS-KB-Q181171 Secure Channel Manipulation with TCP/IP

To set the node type automatically, you can either configure the PC using DHCP, which has a setting for node type:

- MS-KB-Q121005 DHCP Options Supported by Clients

or you can write a small script:

- **MS-KB-Q167640** *Automatically Changing the Node Type of a Windows NT Workstation*

To set the node type manually, modify the Windows Registry key **NodeType**:

- **MS-KB-Q160177** *Default Node Type For Microsoft Clients*

The key is

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netbt\Parameters\NodeType
```

values 1, 2, 4, and 8 correspond to B-node, P-node, M-node, and H-node, respectively. You only need to do that if you want to set the type to P-node or M-node; NT defaults to B-node and enabling WINS changes the type to H-node.

You can also modify the resolution order without changing the node type, using the ServiceProvider Registry key:

- **MS-KB-Q139270** *How to Change Name Resolution Order on Windows 95 and Windows NT*
- **MS-KB-Q187709** *Windows NT 4.0 Domain Name Resolver Caches Responses Regardless of Registry Setting*
- **MS-KB-Q173941** *Windows NT DNR Does Not Cache Short Names*
- **MS-KB-Q171567** *Windows NT 4.0 ServiceProvider Priority Values Not Applied*
- **MS-KB-Q172218** *Microsoft TCP/IP Host Name Resolution Order* describes the difference between “host name resolution” (i.e. DNS name resolution) and NetBIOS-name resolution.
- **MS-KB-Q198550** *SP4 Changes DNS Name Resolution*
- **MS-KB-Q230744** *Windows NT 4.0 SP4 DNR Client Does Not Send Unqualified DNS Queries*

Module 19.7 explained that NetBIOS name resolution can use DNS. An added complication is that if you are running a Microsoft DNS server, you can configure the DNS server to look up WINS if the name to be resolved isn't found in the DNS. For more information see Web Appendix 26.

### Appendices

- Appendix 21: NetBIOS names and suffixes
- Appendix 22: DNS and NetBIOS name resolution order in Windows
- Appendix 23: Windows name resolution worksheet
- Web Appendix 25: Summary of WINSCL.EXE commands
- Web Appendix 26: Microsoft DNS can use WINS

## 20. Windows Networking – logon and domains

- 20.1 Overview of NT domains and security
- 20.2 The logon prompt and local and network logons
- 20.3 Local logon. Encrypting the password
- 20.4 Logon over the network – overview
- 20.5 Logon over the network (1a) – “discover” a domain controller
- 20.6 Logon over the network (1b) – the computer account
- 20.7 Logon over the network (1b contd) – PC authenticates and creates a secure channel
- 20.8 Logon over the network (2) – sending the password securely
- 20.9 Different logon types: terminology (1)
- 20.10 Different logon types: terminology (2)
- 20.11 Logon and controlling access to network resources
- 20.12 Domain controllers
- Summary

### Introduction

This chapter explains how Windows Networking uses “domains” to control user logons and access to resources, and how in logging on to the domain your PC interacts over the network with a “domain controller,” which performs the actual validation of your logon.

We cover these topics in a lot of detail – certainly more than you need in day-to-day operations, (a) because it’s hard to get this information elsewhere, and (b) so that when something goes wrong you can understand what the error messages really mean and use an intelligent approach in resolving your problem. You can skip Modules 20.5–20.10 on first reading if you wish.
