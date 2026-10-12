
**Figure 17.4** Typical FTP implementation

The part of the client program that handles the user interface (or, if it’s a GUI client, the user clicks on buttons, filenames, etc.). This part of the program communicates the user’s instructions to the “protocol interpreter” (PI) – a separate part of the program that sends FTP protocol commands to the server, and interprets responses from the server. The PI also controls the “data transfer process” (DTP) component, instructing it as to when to connect to the server, which IP address and port number to connect on, which files to transfer, etc. The actual file data, directory listings, and so on are transferred over the data connection.

![](img/a2132b646d336d5f9a21102d6320e537_458_0.png)

**Figure 17.5** Client controls third-party transfer between two other machines

![](img/a2132b646d336d5f9a21102d6320e537_458_1.png)

The FTP protocol can handle “third-party” transfers, from one remote server to another remote server, controlled by a client elsewhere (Figure 17.5), which is why the control and data connections are separate. Nowadays this isn’t particularly useful but on the early Internet, before personal computers or workstations were invented, it was used a lot. Often the computer your terminal was connected to was limited in power, and any heavy computation had to be carried out on another machine. Using third-party FTP, you transferred your data from, say, a host controlling lab equipment where experimental data were generated, to a powerful machine to analyze the data. (Then you **telneted** to the powerful machine to run your analysis programs.) Not all clients and servers provide a user interface that lets you specify third-party transfers.

In the next module we look at how the FTP connections are established, and a problem caused by having more than one connection.

### 17.3 How FTP connections are established

A typical FTP session consists of two phases (Figure 17.6):

1. the user specifies to the client which server and port to connect to. The client establishes the control connection. The user logs in, negotiates any transfer parameters with the server (e.g. binary or text mode transfer), and sets any local parameters (whether to print "#" marks for every $n$ data blocks transferred, etc.).
2. the user requests a file transfer (from server to client or vice versa). The data connection has to be established now. The procedure is:
   a. the client opens an ephemeral port and listens on it, waiting for the server to connect
   b. the client sends the **FTP PORT** command, telling the server the number of the port the client is listening on.
   c. the server connects to that port and the connection is established
   d. the data are transferred over the connection
   e. the connection is closed.

Phase 2 is repeated for each transfer (each file or directory listing), using a new data connection each time.

![](img/a2132b646d336d5f9a21102d6320e537_459_0.png)

**Figure 17.6** The two phases of a typical "active mode" FTP session

We can see the connections using `netstat` (with appropriate option to show only TCP connections, for convenience):

```
netstat -n -t
```

(Linux)

```
netstat -n -p tcp
```

(Windows-NT)

Opposite we show the `netstat` output, edited to save space (i) when the client logged in, (ii) during transfer of file-1, (iii) during transfer of file-2, and (iv) when the file transfers were completed. You can see that the control connection (marked "C" in the figure, connecting ports :1067 and :21) persists throughout, but different data connections (D1 = :1068/:20 and D2 = :1073/:20) are used for each transfer and then terminate.

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 192.0.2.19:1067 | 192.0.2.17:21 | ESTABLISHED |

*(i) When client logged in*

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 192.0.2.19:1068 | 192.0.2.17:20 | ESTABLISHED |
| tcp | 0 | 0 | 192.0.2.19:1067 | 192.0.2.17:21 | ESTABLISHED |

*(ii) During transfer of file-1*

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 192.0.2.19:1073 | 192.0.2.17:20 | ESTABLISHED |
| tcp | 0 | 0 | 192.0.2.19:1067 | 192.0.2.17:21 | ESTABLISHED |

*(iii) During transfer of file-2*

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 192.0.2.19:1067 | 192.0.2.17:21 | ESTABLISHED |

*(iv) When file transfers were completed*

The way the data connection is established causes problems when the connection is through a firewall, from an internal client to an external server. The data connection is established from outside the firewall (the server) to inside (the client) on a more or less random port (:1068 here). The firewall doesn't know whether this is the second phase of a genuine FTP session that an internal client established or an outside hacker trying to break in and consequently many firewalls block it.

To overcome this problem, the FTP server can operate in passive mode (as opposed to active mode, that is what we described above):

- the client issues a PASV command (instead of a PORT command)
- the server opens on an ephemeral port, r, and listens for the client to connect
- the server tells the client the number of the port it's listening on
- the client connects to that port.

The rest (Figure 17.7) is as with active mode. The firewall is now happy, because the connection was established from inside, so it can't be a hacker. We'll now explore FTP in detail using telnet as a client, but to do that we need a new tool, netcat, which we describe in the next module.

![](img/a2132b646d336d5f9a21102d6320e537_460_0.png)

### 17.4 netcat (or nc) – the TCP/IP Swiss army knife

> This module and the next are very detailed. Skip them on first reading if you don’t use FTP a lot.
>
> At its simplest **netcat** is like **telnet**:
>
> - it connects to a TCP server that’s listening on a port
> - it reads the input you type and sends it to the server
> - it receives the output that the server returns on the connection, and prints it.

However, **netcat** differs from **telnet** in three important ways:

a. it can listen on a port for incoming connections, and respond to them. In this mode it acts like a server. By contrast, **telnet** always acts as a true client and can only connect to a port that’s already listening

b. it avoids **telnet**’s complexity (fancy options for special modes, terminal handling, etc., which we haven’t covered, as they don’t relate to its network functionality)

c. it can use UDP as its transport instead of TCP.

That gives us four possible modes, which we examine below.

**netcat** is available for Linux and Windows. See Appendix 19 for more details and its manpage. (The name is confusing. It’s referred to as **netcat** but the program, manpage, etc. are all called **nc**.)

#### 1. nc as TCP client (replacement for telnet)

You can use **netcat** to connect to SMTP servers, HTTP servers, etc. as we did in earlier chapters. For example:

```
alice@# nc mail11.microsoft.com smtp
220 inet-vrs-01.redmond.corp.microsoft.com InterScan VirusWall NT ESMTP 3.
```

(One thing you probably *won’t* be able to do is logon to a remote system on the **telnet** port. The **telnet** server goes through a preliminary terminal and parameter negotiation with the client, and doesn’t issue the login prompt until that has succeeded, and **netcat** doesn’t bother with this by default. However, if your **netcat** version supports the “-t” option, it gets round this problem.)

#### 2. nc as TCP server

This is the mode that we need in the next module. Use options “-l” (listening mode, i.e. server) and “-p *portnum*” (port number to listen on), e.g.

```
nc -l -p 80        # may not work if Web server already running
```

listens on port 80, i.e. can be used as a dummy or test Web server, at least to detect incoming connections. (If you have another process, such as a real Web server, already listening on port 80, **netcat** will fail because it won’t be allowed access to port 80.) Check that **netstat** is doing
