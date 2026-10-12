
Complex filtering statements may be constructed through the use of primitives grouped together with logical operators and parenthesized expressions.

Logical operators allow multiple filtering primitives to be examined in a comparative fashion. Table 16.6 lists the logical operators that are supported.

## Table 16.6 Network Traffic Filtering Operators

| Operator | Description |
|---|---|
| !, not | Negation operators. These evaluate as true only if their associated primitive statement results in a false return value. |
| &&, and | Concatenation operators. These operators require two primitive statements, evaluating as true if both primitives result in a true return value. |
| ||, or | Alternation operators. These operators require two primitive statements, evaluating as true if one or both primitives result in a true return value. |

Logical operators are used in the following manner:

```
[Primitive] [Operator] [Primitive]
```

Example: port ftp && host 192.168.1.5

Parenthesized expressions allow groups of filtering expressions to be evaluated together as a single "virtual" primitive. This "virtual" primitive can then be used in higher-level filtering evaluations. Parenthesized expressions are used in the following manner:

```
( [Expression] )
```

Example: ( port ftp )

Primitives, logical operators, and parenthesized expressions may all be used in combination to allow for extremely complex multi-leveled packet filtering activity. Examples of these elements in combination are

```
( port ftp ) || ( port http ) && host 192.168.1.4
( port http ) || ( port http )
```

The use of filtering expressions makes monitoring specific types of network traffic an easy task. They provide complex kernel-space packet analysis capabilities, off-loading any sort of filtering activity from having to take place in a user-space network monitoring system. This provides faster performance levels and simplifies monitoring software source code, as the monitoring system itself doesn't have to worry about any sort of packet filtering tasks.

Using the expression writing techniques outlined in this section, any type of data traffic traveling over a network may be captured and examined. These expressions provide for virtually unlimited filtering capabilities.

## Summary

Network monitoring can be a powerful tool for detecting attacks against active hosts, determining network bottlenecks, and for providing a general in-depth view into the activity occurring on your network. The techniques described in this chapter will enable you to deploy and use such monitoring systems successfully on a computer network.

## Integrating with Windows NT Networks

### In This Chapter

- Networking the Windows Way 462
- Linux and Samba in an NT Environment 464

With Linux making inroads into the corporate network environment, interoperability with existing network operating systems is critical and Linux does a good job of this. This chapter looks at how Linux and Windows can communicate with each other using one of the most exciting software products available for Linux today, Samba. We will first review the essentials of Windows networking and the terms used in describing them and then look at setting up Linux and Samba to act as either a client or server in a Windows network.

## Networking the Windows Way

The networking support contained in Windows 98 and Windows NT is the result of years of evolution that had its beginning with the NetBIOS file-sharing protocol developed by IBM in the early days of personal computing. This simple protocol was enhanced over the years to eventually become the Session Message Block, or SMB, protocol and finally the Common Internet File System, or CIFS. To get a better understanding of the manner in which Windows networking works, let us start with some definitions and then take a look at a simple network setup using Windows NT to provide file and print services to Windows 98 clients.

### Speaking the Lingo

One of the keys to understanding any technology is to understand the terminology used by practitioners of that technology. This section defines some of the terms used in describing Windows networks. The intention is not to make you fluent in the language of Windows networks, but merely to cover a few of the terms that you need to know in order to set up Samba.

A workgroup or domain refers to a group of machines on a network that query a common browsing database of shared resources. The primary difference between a workgroup and a domain is that a domain shares security information and a workgroup does not. Every Windows network consists of one or more workgroups or domains and your setup must define a domain or workgroup for Samba.

Browsing refers to the act of accessing the common database via whatever interface the operating system provides. For Windows 98 and Windows NT, this interface is usually the Windows Explorer. The browsing interface for OS/2 is the Workplace Shell and for Linux it is smbclient.

A master browser is the machine in a domain or workgroup that maintains the shared resources database that other members of the group browse. There are two types of master browser:

- The *domain master browser* holds the master browsing database for an entire domain, which may span one or more subnets.
- The *local master browser* holds the master browsing database for a local subnet and queries the domain master browser for information on resources on other subnets.

### A Simple NT Network

To better understand how Linux and Samba can integrate into your network, let's first examine a simple Windows network, looking at each piece and seeing how they fit together. Our network will consist of a single domain. A Windows domain consists of the following parts:

- One primary domain controller (PDC)
- One or more backup domain controllers (BDC)
- One or more resource servers
- Participating clients

For purposes of our examples, our network will be centered on a Windows NT server that acts as the primary domain controller (PDC). The PDC is responsible for validating user logons to the domain and maintaining the central user database. It is also the maintainer of the security policies database and is the administrative unit for the network. In addition to these roles, this system may also be a resource server, sharing filesystems, printers, or other resources with client systems on the network.

The next machine in our network is another Windows NT server that acts as the backup domain controller (BDC). The BDC also maintains a copy of the user database and security policies database, which it replicates from the PDC, and shares the task of authenticating users. It is intended to provide redundancy in the event that the PDC is unavailable. Again, as with the primary domain controller, the backup domain controller may also be a resource server for the network.

We have one other server in our network that is strictly a resource server. It is a file and print server, email server, and also serves as the intranet Web server. It is often desirable to separate the functions of primary and backup domain controller from the resource sharing function so that a problem with your resource server does not prevent people from logging into the network. This machine does not handle user authentication directly, but passes authentication requests to the primary domain controller. Some of the shared resources served by this machine are the two network printers. Even though these printers are not connected directly to the server, access to the printers is managed through it for accounting purposes.

The majority of the machines on this network are client systems running Windows 98 or Windows NT Workstation, as well as a few OS/2 systems. Figure 17.1 illustrates this

![](img/4886c42c7629f445c7f7f3011ffbf3c3_497_0.png)

## Linux and Samba in an NT Environment

[Text unclear due to image blur]
