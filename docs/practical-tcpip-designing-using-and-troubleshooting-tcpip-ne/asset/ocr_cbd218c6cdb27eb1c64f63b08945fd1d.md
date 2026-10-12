# ## Summary

+   * the daytime, echo, chargen, and discard little services are useful for testing

+   * FTP is the traditional way to transfer files over the network:
+       - it runs over TCP
+       - it uses separate control and data channels
+       - client and server exchange command and control information as plain text strings on the control channel
+       - normally it is the server that establishes the data connection to the client. This causes problems with firewalls, which can be overcome by using passive mode

+   * the netcat (or nc) tool is useful for testing FTP and many other services

+   * X is a client/server window system used on Linux and almost every UNIX version, and on many other platforms

+   * LDAP allows directories of users, passwords, e-mail addresses, machine details, and other information to be retrieved over the network from a central database. LDAP is at the core of Windows-2000 Active Directory and many other user/configuration management systems

+   * SNMP lets you remotely monitor and manage machines and devices on your network

+   * Syslog is the system logging service; messages are logged to a central server instead of to a local file

+   * lpr is the Linux/UNIX network-based printing service

+   * NTP lets you synchronize the clocks on your machines across the LAN, WAN, or Internet

+   * NFS is the Linux/UNIX filesharing system. It lets a client machine mount a directory that lives on a remote NFS server and access its files as though they were on a local disk.

# ## What’s next?

We’ve reached the end of Part 2, which covered the common TCP/IP applications and their protocols, which are used on almost every platform. In Part 3, we look at Microsoft Windows Networking – what it is, how it works, and how it ties in with the rest of your TCP/IP network.

# ## Notes and further reading

# ### Daytime, echo, chargen, discard

There are many other services listed in a typical /etc/services (Linux) or C:\winnt\system32\drivers\etc\services file (NT) that are rarely used. Some, such as quotd (“quote of the day”) were and still are merely curiosities. Others, like webster (server for Webster’s dictionary) shared an expensive resource to many machines over the network, and have been largely supplanted by equivalent facilities on the Web. Still others (finger, netstat, systat) gave information on users and systems, but are not often used now, both because they can give information to potential hackers and because there are other ways for legitimate users to get the information they need.