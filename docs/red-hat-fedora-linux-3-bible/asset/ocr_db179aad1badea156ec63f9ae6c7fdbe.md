> **CROSS-REFERENCE:** Only the ssh service is turned on by default in Fedora Core. That is because the other remote login, execution, and copy commands described here do not provide encrypted communications by default, and so they can represent significant security risks. For information on how to turn on the services described in this chapter on a Fedora Core server, refer to Chapter 14 and Appendix C.

Two of the commands described in this section are generally available are remote login and file transfer programs: *telnet* and *ftp*, respectively. Other commands for accessing FTP servers are *ncftp* and *gFTP*.

Two newer commands for copying files over the network are *wget* and *rsync*. Both of these tools can be used for efficiently downloading files that you can identify on the network.

Other commands described in this section are more specific to Fedora Core and other UNIX systems, but they provide simplified ways of copying files, logging in, and executing commands among trusted systems: *rcp*, *rlogin*, and *rsh*, respectively. Also, a more secure tool for remote login, called *ssh*, is included with Fedora Core. The *ssh* command can be used for remote execution as well.

# Using telnet for remote login

Telnet is a service provided by many different types of computer systems to enable remote users to log in to their machines over TCP/IP networks. The *telnet* command is the client program that you use to do the remote login. The most common way to use telnet is with a host name. The following is a typical telnet session:

```
```text
$ telnet maple
Trying 10.0.0.11 ...
Connected to maple.linuxtux.net (10.0.0.11).
Escape character is '^l'.
Fedora Core release 3
Kernel 2.6.8-1 on an i686
login: mike
Password: *******
Last login: Mon Nov 28 13:15:57 from pine
[mike@maple mike]$ ```
```

This example shows what happens when the *telnet* command is used to log in from a computer named *pine* to a computer named *maple* by typing *telnet maple*. My computer tries to connect to the telnet port on *maple* (IP address `10.0.0.11`). Because *maple* is also a Fedora system, once the connection is established, I see the standard *login:* prompt. I type the user name (*mike*) and the password when prompted. When the login and password are accepted, I see the shell prompt for the user *mike*.

The telnet service is disabled by default on Fedora Core systems (as are most network services). So, to be able to log in to your computer using telnet, refer to Appendix C for information on how to turn on the telnet service.