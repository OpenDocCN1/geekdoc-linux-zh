for people—they do not change how computers use TCP/IP to communicate among themselves. When you use a name instead of an address in an application, the computer must convert the name into the proper IP address before initiating communication with the target computer. This name-to-address conversion is called **name resolution**. For example, when you key the name of an Internet server into your Web browser, the browser must resolve that name into an IP address. After the computer has the address of the Internet server, it can send its first message through TCP/IP, requesting access to the resource that you specified in the browser.

The **Domain Name System (DNS)** is the name resolution mechanism computers use for all Internet communications and for private networks that use the Active Directory domain services included with Microsoft Windows Server 2008, Windows Server 2003, and Windows 2000 Server. The names that you associate with the Internet, such as the names of Internet servers in Uniform Resource Locators (URLs) and the domain names in email addresses, are part of the DNS namespace and are resolvable by DNS name servers. Windows Server 2008 includes its own DNS server that you can deploy on your private network.

Windows operating systems prior to Windows 2000 used **NetBIOS names** to identify the computers on the network. The NetBIOS name of a computer running Windows is the name you assign to it during the operating system installation. Windows includes Internet name resolution mechanisms for NetBIOS systems, including **Windows Internet Naming Service (WINS)**. Starting with Windows 2000, Windows operating system releases rely on Active Directory and DNS instead of NetBIOS names. However, all Windows operating systems still include a WINS client to resolve NetBIOS names. Windows Server 2008, Windows Server 2003, and Windows Server 2000 all include a WINS server so they can provide NetBIOS name resolution for networked computers and applications that are running previous operating systems or that still have a reliance on NetBIOS name resolution.

The processes by which friendly names are associated with IP addresses and the mechanisms used to perform name resolution have evolved over the years. When the Internet was established in 1969 as an experimental wide area network (WAN) named ARPA- NET by the United States Defense Advanced Research Project Agency (ARPA), system administrators assigned single-word friendly names to their computers. These friendly names, called **host names**, represented the computer's IP address in applications and other references. Today, the term **host** refers to any device on a TCP/IP network, such as a printer, scanner, or computer, that has an IP address; a DNS **host (A)** record defines a host on an IPv4 network.

One method of resolving host names into IP addresses uses a hosts file. A hosts file is a text file called **hosts** that contains a list of host names and their equivalent IP addresses, similar to the following list:

```
```
172.16.94.97    server1    # source server
10.25.63.10     client23   # x client host
127.0.0.1       localhost
```
```

The host table consists of three columns, which list the following information, from left to right:

+   * **IP address.** The IP address of a particular system on the network.
+   * **Host name.** The host name associated with the IP address in the first column.
+   * **Comments.** The computer ignores everything after the # symbol when it scans the host table. Administrators use this space to add comments, such as a description of the system that the IP address and host name in the first two columns represent.

When an application encounters a reference to a host name, it consults the computer's hosts file, searches for the name, and reads the IP address associated with that name. Every computer that uses TCP/IP contains a host table. The advantage of using a hosts file for name resolution is simple and fast resolution. Because the file is stored on the computer's local