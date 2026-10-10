# Block and Stop Unnecessary Services

Some services are configured to accept connections from any source IP address. For example, an HTTP server for an e-commerce organization must accept connections from any IP address in order to allow remote users in all locations to view the organization’s web site. In such a case, it is impossible for an organization to hide the fact that they are running an HTTP server.

However, depending on the organization’s requirements and network architecture, some services may only expect connections originating from authorized IP addresses. In such cases, firewall rules should be put in place to ensure that connections originating from unauthorized IP addresses are blocked. In addition, unnecessary services must be turned off or blocked by firewall rules. This will prevent the exploitation and identification of services that should not be accessible by unauthorized remote hosts.

# FTP (File Transfer Protocol): 21 (TCP)

FTP, as the name suggests, is a protocol for transferring files from one host to the other.

# Obtain the FTP Server Banner

FTP servers usually print version information when connected to. An FTP client can be used to connect to an FTP server in order to obtain its banner. For example:

```
(bash)$ ftp 192.168.1.1
Connected to 192.168.1.1 (192.168.1.1).
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
Name (192.168.1.1:username):
```

The telnet client can also be used to connect to the FTP port directly to obtain the banner information:

```
(bash)$ telnet 192.168.1.1 21
Trying 192.168.1.1...
Connected 192.168.1.1.
Escape character is '^'.
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
```