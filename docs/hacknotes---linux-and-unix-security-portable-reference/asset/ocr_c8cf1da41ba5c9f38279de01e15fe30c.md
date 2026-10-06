# FTP Bounce Scans

Due to the design of the FTP protocol, when an FTP client requests data transfer using "active" mode, the FTP server must initiate a connection back to the FTP client. FTP clients issue a PORT command with their IP address and listening port number as parameters. If the FTP client issues a PORT command with the IP address of another host, the FTP server will attempt to connect to that host. Therefore, this feature of the FTP protocol can be used to proxy scans.

The nmap command includes a -b flag to perform "FTP bounce" scans:

```
nmap -b username:password@ftp.somecompanyexample.com:21 -p 4000-8080 target.somecompanyexample.com
```

> FTP clients may use passive mode when requesting data transfer, which will cause the FTP client to connect to a port on the FTP server in order to perform the data transfer. However,passive-mode FTP has its own problems. Passive-mode FTP clients may be subject to "connection theft" vulnerabilities. Please see Chapter 4 for details.

# TCP SYN/Half-Open

This type of scanning causes the scanner to send out a SYN packet to the target host. If the target host is listening on a particular port, it will respond with a SYN+ACK. If alive, a RST packet will be received. As this method of scanning does not complete the TCP three-way handshake, it is stealthy; since it is not logged by the target host.

# SYN Scanning

Using -sS flag in nmap will perform a SYN scan:

```
[bash]# nmap -sS 192.168.1.150
nStarting nmap V 3.00 ( www.insecure.org/ )
Interesting ports on (192.168.1.150):
(The 1599 ports scanned but not shown below are in state: closed)
Port    State   Service
22/tcp open    ssh
113/tcp open    auth

Nmap run completed -- 1 IP address (1 host up) scanned in 2 seconds
```