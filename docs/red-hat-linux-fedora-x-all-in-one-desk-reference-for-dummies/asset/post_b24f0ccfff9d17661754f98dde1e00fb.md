
# Understanding Internet Services 601

from to five connections. However, the size of the listen queue is one of the parameters you can adjust (especially for a Web server) to ensure that the server responds to as many clients as possible. After setting up the listen queue, the server waits for a connection from a client.

Establishing the connection from the client side is somewhat simpler. Creating a socket and binding the socket to an IP address, the client establishes connection with the server. To make the connection, the client must know the host name or IP address of the server, as well as the port on which the server accepts connection. All Internet services have well-known standard port numbers.

![](img/d9230b719dc0efd80851f363d8c6f571_627_0.png)

After a client establishes a connection to a server via a connection-oriented stream socket, the client and server can exchange data by calling the appropriate API functions. Like a conversation between two persons, the server and client send and receive data—the meaning of the data depends on the message protocol the server and clients use. Usually, a server is designed for a specific task; inherent in that protocol that the server and clients use to exchange necessary data. For example, the Web server and the Web browser communicate using the HTTP (HyperText Transfer Protocol).

# Internet services and port numbers

The TCP/IP protocol is the lingua franca of the Internet because the Internet services "speak" TCP/IP. These services make the Internet tick by making possible the transfer of mail, news, and Web Pages. Each Internet service has its own protocol that relies on TCP/IP for the actual transfer of information. Each service also has one or more assigned port numbers that it uses to do whatever it is designed to. Here are some well-known Internet services and their protocols:

- DHCP (Dynamic Host Configuration Protocol) is for dynamically configuring TCP/IP network parameters on a computer. DHCP is primarily used to assign IP addresses and other networking information such as name server, default gateway, domain names that are needed to configure TCP/IP networks. The DHCP server listens on port 67.

- FTP (File Transfer Protocol) is used to transfer files between computers over the Internet. FTP uses two ports—data is transferred on port 20; control information is exchanged on port 21.

- HTTP (HyperText Transfer Protocol) is for sending documents from one system to another. HTTP is the underlying protocol of the Web. By default, the web server and client communicate on port 80.

- SMTP (Simple Mail Transfer Protocol) is for exchanging e-mail messages between systems. SMTP uses port 25 for information exchange.

![](img/d9230b719dc0efd80851f363d8c6f571_627_1.png)

# 602 Understanding Internet Services

- NNTP (Network News Transfer Protocol) is for distribution of news articles in a store-and-forward fashion across the Internet. NNTP uses port 119.

- SSH (Secure Shell) is a protocol for secure remote login and other network services over an insecure network. SSH uses port 22.

- TELNET enables a user on one system to log in to another system (the user must provide a valid user ID and password to log in to the remote system). TELNET uses port 23 by default. However, the TELNET client can connect to any specified port.

- NFS (Network File System) is for sharing files among computers. NFS uses Sun's Remote Procedure Call (RPC) facility, which exchanges information through port 111.

- NTP (Network Time Protocol) is used by client computers to synchronize the system time with that of a server (one with a more accurate clock). NTP uses port 123.

- SNMP (Simple Network Management Protocol) is for managing all types of network devices on the Internet. Like FTP, SNMP uses two ports: 161 and 162.

- TFTP (Trivial File Transfer) is for transferring files from one system to another (typically used by terminals and diskless workstations) to download boot files from another host on the network). TFTP data transfer takes place on port 69.

Each service is provided by a server process — a program that runs on a system awaiting client requests that arrive at the well-known port associated with its service. Thus the Web server accepts requests at port 80, the standard port for HTTP service.

The /etc/services text file on your Fedora Core system stores the association between a service name and a port number (as well as a protocol). Here is a small subset of entries in the /etc/services file from a Fedora Core system:

```
ftp-data        20/tcp
ftp             21/tcp          # SSH Remote Login Protocol
sh              22/tcp          # SSH Remote Login Protocol
sh              22/udp
telnet          23/tcp
smtp            25/tcp          mail        timserver
time            37/tcp          timserver
time            37/udp
rlp             39/udp          resource    # resource location
nameserver      53/udp          name        # IEN 116
whois           43/tcp          nicname
```

# Using the xinetd Super Server 603

A quick look through the entries in the /etc/services file shows the breadth of networking services available under TCP/IP.

Note: Port number 80 is designated for Web service. In other words, if you set up a Web server on your system, the Internet Assigned Numbers Authority (www.iana.org) is responsible for the assignment of port numbers below 0.

![](img/d9230b719dc0efd80851f363d8c6f571_629_0)

# Using the xinetd Super Server

The xinetd architecture requires that the server be up. The idea is that the /etc/xinetd.d directory contains service-configuration files — one file for each service xinetd is expected to manage. The last line in /etc/xinetd.conf includes the includirect to include all files in /etc/xinetd.d, excluding files that begin with a period (.).

Here is the listing of files when I run the ls /etc/xinetd.d on a Fedora system (the exact content of /etc/xinetd.d depends on the Internet services installed on your system):

+   chargen-udp
+   cups-lpd
+   daytime-udp
+   echo-udp
+   finger
+   ktalk
+   rsync
+   sgm
+   telnet
+   time-udp

Each of these files specifies the attributes for one service. For example, the following listing shows the contents of the /etc/xinetd.d/telnet file, which specifies the xinetd configuration for the TEL service:

```
# description: The xinetd serves Telnet sessions; it uses
# encrypted username/password pairs for authentication.
telnet service
{
    flags = REUSE
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/in.telnetd
    log_on_failure = ++USERID
    disable = yes
}
```

The filename (in case, telnet) can be anything; what matters the service name that appears to the service in the file. the line service telnet tells xinetd the name of the service. xinetd uses this name to look up the port number from the /etc/services file. To look for telnet in the /etc/services file, type the following command:

```
grep "telnet" /etc/services
```

The command displays the following lines:

```
telnet 23/tcp
telnet 23/udp
telnets 992/tcp
telnets 992/udp
```

# 604 Using the xinetd Super Server

The /etc/xinetd.conf file is the configuration for the xinetd daemon. Comment lines begin with the pound sign (#). The defaults block of attributes, enclosed in curly braces ({ }), specifies default values for some attributes. The instances attribute is set to 60, which means, at most, 60 servers can be simultaneously.

![](img/d9230b719dc0efd80851f363d8c6f571_630_0)

The last line in /etc/xinetd.conf includes the includirect to include all files in /etc/xinetd.d, excluding files that begin with a period (.).

Book VIII
Chapter 1
Managing the Servers
