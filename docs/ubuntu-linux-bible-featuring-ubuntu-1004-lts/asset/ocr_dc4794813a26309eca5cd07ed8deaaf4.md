# Part II: Ubuntu for Desktop Users

authentication information and all other data exchanged between a telnet client and a server are exchanged in the clear, meaning that it is readily visible to anyone with access to your network, a packet sniffer, and sufficient curiosity or other motivation. There are ways around this, of course. You can use telnet through an encrypted virtual private network (VPN) tunnel or install a version of telnet that uses Kerberos authentication, but why cling to an old application and protocol when there are newer, more secure alternatives available? (If you're still fascinated with telnet, search the Web for information about Linux VPNs or see Chapter 27, "Managing Users, Groups, and Authentication," for information about installing Kerberos on your system, which includes a Kerberized version of telnet.)

# Tip

The telnet client is installed as part of a default Ubuntu installation because you may need the telnet client to connect to other systems or systems that do not support more sophisticated connections, but a telnet server is never officially supported by Ubuntu. If you must, you can still explicitly install the telnet server—known as telnetd—from a "universe" repository you use your favorite package management software.

> If you're an old-time UNIX user, you may remember the Berkeley r-command suite, which provided voted commands using ssh and rcp. These commands had the same security problems as the older telnet commands, namely, they transmitted passwords and other information in the clear. Although these commands appear to be available on Ubuntu Linux systems, they are mapped to the corresponding commands (ssh and rcp, respectively) using the alternatives system that is discussed in Chapter 19, "Adding, Removing, and Updating Software."

# Logging in Remote Systems using ssh

The newer, more modern and secure replacement for telnet is ssh, the secure shell application, which uses SSH, the Secure Shell protocol. The ssh application is installed as part of a default Ubuntu Linux installation, with other applications that use the same protocol and authentication information, and shares much of the command-line syntax, such as sftp (a remote File Transfer protocol). Using ssh, you can establish a remote login session on any machine that is running an ssh daemon. An ssh daemon must be running on the remote system. If you try to connect to the remote system and see a message like following, either an ssh daemon is not running on that system or it is running on some other port than the default port 22:

```
$ ssh uaptlop
ssh: connect to host uaptlop port 22: Connection refused
```

The remainder of this section discusses how to use ssh to connect to remote systems that are actually running an ssh daemon. For information on how to enable the ssh daemon on Ubuntu systems, see the next section.

Using ssh to connect to a remote system as the current user is as simple as typing the ssh hostname command, where hostname is the name or IP address of the host you want