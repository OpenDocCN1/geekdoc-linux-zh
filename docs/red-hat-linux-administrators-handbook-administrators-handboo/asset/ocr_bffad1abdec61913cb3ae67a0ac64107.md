```
server:  process in.telnetd
matched: /etc/hosts.deny line 10
access:  denied
```

This utility allows you to test your tcpd configuration quite thoroughly. The TCP wrapper is a must if you are going to run inetd on your system. More information about tcpd and its configuration can be obtained by reading the tcpd (8), tcpdchk (8), tcpdmatch (8), hosts.allow (5), and hosts_options (5) man pages. You can also find the tcpd source at http://www.cert.org/ftp/tools/tcp_wrappers/.

# Replacing the r commands with Secure Shell (ssh)

If you do not use the r* commands, including rlogin, rsh, rexec, and so on, consider removing them completely from your system. You can comment out the lines specific to r* commands in the /etc/inetd.conf file to ensure that the services these commands provide are no longer available.

If you use these services to access your system, consider replacing them with a secured solution called Secure Shell or ssh, which gives you all the benefits of the r* commands (and then some). For example, using ssh, you can log in to a remote system or execute a command on the remote system using a secured, encrypted connection. It provides extensive logging capabilities and works well with syslog. With ssh, you can also create secure remote X sessions. It can provide protection against IP and DNS spoofing, attacks based on the weaknesses in the X authentication protocol, and so on. You can get ready to run RPM packages for ssh from the following Web site: http://www.replay.com/redhat/ssh.html.

You need the base ssh package, the ssh client package, and the ssh server package. U.S. export control laws for encryption software may place some legal restriction on ssh, so make sure you read the documentation found in the preceding Web site.

# Protecting Your Files and File System

One of the best way to ensure file and filesystem security is to provide least privileged access to them. If users can get by with read access only, then