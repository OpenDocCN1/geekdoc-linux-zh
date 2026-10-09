# # FTP Servers

Various FTP servers provide different FTP services.

![](bbox=[0.76, 0.09, 0.88, 0.16])

| FTP Server | Description |
| :--- | :--- |
| **Pure-FTPd** | Provides an easy, quick, and secured way of transferring files among the UNIX-based operating systems such as Linux, OpenBSD, NetBSD, and Solaris. The pure-ftpd.conf file is used to configure Pure-FTPd and is stored in the /etc/pure-ftpd directory. |
| **ProFTPd** | Provides an easy way of transferring files among multiple virtual FTP servers. It runs as a standalone server and provides chroot capabilities depending on the filesystem. The proftpd.conf file is used to configure ProFTPd and is stored in the /etc directory. The proftpd.conf file is similar to Apache's configuration file. |

# ## FTP Configuration Files

The FTP configuration files are created and stored with respect to the FTP server that is configured. It contains directives and comments. Directives control the login behavior and access mechanism, anonymous user access to the server, and local user access. The directive name is followed by an equal operator and a value. There should be no space on either side of the equal operator. The comments begin with a # symbol. For example, anonymous_enable=\nYES

```
# Allow anonymous FTP?
```

# ## FTP Connection Modes

An FTP connection between a client and a server can be established through two basic modes.

![](bbox=[0.76, 0.62, 0.9, 0.68])

| Mode | Description |
| :--- | :--- |
| **Active** | In the active FTP mode, the client sends a signal to the server, specifying the port through which the server should connect. The server in turn connects to the client through the specified port. |
| | This mode was developed when firewalls were not common. With the widespread implementation of firewalls, it was found that many problems arose because firewalls blocked the server from establishing a connection with the client. |
| **Passive** | In the passive FTP mode, the client confirms the port with the server and then initiates the connection with it. Because the connection is established by the client, it is not blocked by the firewall. |