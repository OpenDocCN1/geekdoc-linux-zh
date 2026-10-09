Telnet, similar to the FTP program, sends the passwords in clear text during authentication. Because of this, most servers have the telnet server turned off and, instead, use the SSH protocol packages. OpenSSH has a client program called ssh. Like FTP, ssh connects to the remote server, and the remote server exchanges a key with the client, then uses it during communications to encrypt data. The basic syntax of ssh is **ssh servername**, where *servername* is the name of the server to which you want to connect.

```
$ ssh Styx
The authenticity of host 'styx (192.168.0.21)' can't be established.
RSA key fingerprint is 5d:89:60:1b:1e:98:81:4b:ab:bb:e2:d0:8f:42:d8:46.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'styx' (RSA) to the list of known hosts.
root@styx's password:
Last login: Wed Oct 15 13:59:17 2003 from universi-253385.cs.ua.edu
#
```

The first time you connect to a server, a key will be sent by the remote server and you will be prompted to accept the key. The key is used in the encryption process. After you connect to the remote server, you run commands the same way you would on the local machine. To end the remote session type **exit**.

Remote access to Linux servers can be done from almost any operating system. For example, a freely available program called putty, a telnet/SSH client, is available for Windows on Intel x86 and Alpha platforms. Similar programs are available for Apple, Sun, and other computer systems.

Remote access is often used for administration of a Linux system. From a remote shell, you can do anything that you can from a local shell. Other tools provide a GUI interface and some provide HTTP support. HTTP support means that you can access the configuration tools with a browser interface. One such program is Webmin, available from www.webmin.com. Webmin is distributed under a BSD license, meaning that it can be freely copied for any use.

+   - **Objective 2.17**

![](bbox=[0.22, 0.55, 0.28, 0.6])

# ## RMON

The RMON protocol is a network management protocol that allows network information to be gathered at a single workstation. A similar protocol, SNMP (Simple Network Management Protocol), gathers network data from a single type of Management Information Base (MIB). The RMON 1 protocol defines nine additional MIBs that provide a much richer set of data about network usage. Network hardware must be RMON enabled for the protocol to work.

# # FIREWALLS

Security has one purpose—to protect resources. One way to make a computer system more secure is to use strong passwords. Strong passwords ensure that the users requesting services from servers are who they say they are. It may surprise you to know that passwords alone won’t keep the bad guys out. Many protocols run on the server that, left unchecked, prove to be an open door to more experienced users.

The most secure system is one that provides no access to the outside; in today’s environment, however, systems often require outside access. For example, a file server must expose its resources to clients in order to do its job; a Web server must provide outside access to its Web pages; an e-mail server must provide outside access to transport e-mail from server to client; and there are many other examples. The trick to security is to provide access only to the resources necessary to get the job done.

One way to restrict resource exposure is to use a firewall. A firewall on a computer system enforces an access control policy between network resources. A firewall is placed between a trusted network and an untrusted network (Figure 7–34). Firewalls fall into two categories—hardware and software.