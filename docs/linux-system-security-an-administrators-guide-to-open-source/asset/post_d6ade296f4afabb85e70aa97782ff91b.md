
If the service is invoked through inetd, you need to comment out or remove the appropriate entry for the `/etc/inetd.conf` and then inform `inetd` of the changes you've made. For example, suppose that you want to disallow *rlogin* requests from all clients. Edit the `/etc/inetd.conf` file and change the entry

```
login stream tcp nowait root /usr/sbin/tcpd in.rlogind
```

to the following, by simply adding the `#` comment character at the beginning of the line,

```
#login stream tcp nowait root /usr/sbin/tcpd in.rlogind
```

Then inform `inetd` of the change by executing

```
# killall -HUP inetd
```

Now, `inetd` will refuse all requests for `in.rlogind` which supports the *rlogin* client-side program.

Some services have numerous vulnerabilities. Table 3.1 lists many of the services available and recommends whether or not they should be made available. It also lists the default state (On or Off) and the port number with which it is associated.

### Table 3.1 Standard Services and Recommended Usage

| Service | State/Port | Description of Function | Recommended Use |
| --- | --- | --- | --- |
| chargen | Off/19 | Generates ASCII data for debugging purposes. | Leave it off. |
| daytime | Off/13 | Provides day and time in ASCII. | Normally not necessary. Leave it off. |
| discard | Off/9 | Discards any data received. Used for debugging. | Leave it off. |
| echo | Off/7 | Echoes back all data received. Used for debugging. | Leave it off. |
| ftp | On/21 | File Transfer Protocol for transferring files over the network. | Often a required service. |
| gopher | On/70 | Command-line based predecessor to web browsers. | Normally not used. Turn it off. |
| smtp | Off/25 | Simple Mail Transfer Protocol | Required for POP; otherwise leave it off. |
| nntp | Off/119 | Network News Transfer Protocol | Necessary only if the system will be a network news server. |
| shell | On/514 | Supports the remote shell service. | Turn it off. Replace with sshd. |
| login | On/513 | Supports the remote login service. | Turn it off. Replace with sshd. |
| exec | Off/512 | Supports remote command execution through rexec. | Leave it off. |
| talk ntalk | On/517 On/518 | Provides for text based interactive communications. | Turn them off. Use Internet relay chat (IRC) or e-mail. |
| imap | On/143 | Internet Message Access Protocol e-mail services. | Unless the system is an IMAP server, turn it off. |
| pop-2 pop-3 | On/109 On/110 | Provides Post Office Protocol (POP) e-mail services. | Unless the system is a POPv2 or POPv3 mail server, turn these off. |
| uucp | Off/117 | UNIX-to-UNIX copy provides batch-oriented and on-demand file transfer service. | Unless the system must provide uucp services, turn it off. |
| tftp | Off/69 | Trivial File Transfer Protocol. A simplified version of ftp that performs no authentication checking. | Used only for systems that will act as install or diskless client servers. |
| bootps | Off/67 | Provides booting service for network clients, such as X-terminals and diskless nodes. | Used only for systems that will act as a boot server. |
| finger | On/79 | Provides user information. | Turn it off unless specially configured for DMZ operations. |
| systat | Off/11 | Provides system information via ps. | Leave it off. |
| netstat | Off/15 | Provides network statistics via netstat. | Leave it off. |
| time | On/37 | Used for time synchronization of hosts through the remote execution of commands such as rdate or ntp. | This may be necessary for host clock synchronization. |
| auth | On/113 | Provides connection ownership information. | Normally this service is turned on for systems attached to the Internet. |
| linuxconf | On/98 | Provides system administrative graphical user interface (GUI) over the network. | Unless absolutely necessary, turn it off. |
| portmap | On/111 | Not controlled through inetd. | Used for remote procedure call (RPC) services. Usually necessary. Discussed further in *Remote Procedure Call Applications* on page 36. |
| mountd | On/635 | Not controlled through inetd. | Necessary for NFS services. Also required by CFS and TDFS discussed in Chapter 15. If you aren't using any of these services, turn it off. |

If you are unfamiliar with inetd, you really must minimally read *TCP/IP Network Administration* cited in *General TCP/IP Networking Resources* on page 39. For even greater understanding, check out some of the other references noted in that section.

### Remote Procedure Call Applications

There are a variety of services, including NFS and Network Information Services (NIS) (see *Some Major Applications* on page 37), that use remote procedure calls (RPC) to manage the communication, including port use. RPC applications are invoked through the portmap daemon (discussed in Chapter 10). The portmap daemon will supply a port number for the requested service, and that number will be used for the duration of the communication. As with the other topics in this chapter, RPC is a topic with which you should be familiar. If you are not, check out some of the resources noted in *General TCP/IP Networking Resources* on page 39.

### Trusted Host Files and Related Commands

In this section, we will provide an overview description of the behavior of the `$HOME/.rhosts`$, `/etc/hosts.equiv`, and `$HOME/.netrc$${}^{6}$ files, which we collectively refer to as trusted host files. These files are server-side files and related to the server-side daemons in `rlogind`, `in.rshd`, `in.rexecd`, and `in.ftpd`. The related client-side applications are `rlogin`, `rsh`, `rcp`, `ftp`, and `rexec` (often referred to collectively as the r-commands or Berkeley r-commands, as they are derived from the Berkeley System Distribution [BSD]). Table 3.2 provides a list of trusted host files and their application associations.

| Client-Side Application | Server-Side Daemon | Server-Side Trusted Host Files |
| :--: | :--: | :--: |
| rlogin | in.rlogind | /etc/hosts.equiv<br>`$HOME/.rhosts$` |
| rsh | in.rshd | /etc/hosts.equiv<br>`$HOME/.rhosts$` |
| rcp | in.rshd | /etc/hosts.equiv<br>`$HOME/.rhosts$` |
| ftp | in.ftpd | `$HOME/.netrc$` |
| rexec | in.rexecd | `$HOME/.netrc$` |

6. The shell environment variable HOME contains the home directory of the user.

The `/etc/hosts.equiv` file provides an authentication database for non-root users. The `$HOME/.rhosts` and `$HOME/.netrc` files provide authentication databases for the users in whose home directories they reside. The purpose of these files is to provide user authentication without requiring a password.

The syntax of the `$HOME/.netrc` file is documented in the `tcp(1)` man page. The syntax of the `/etc/hosts.equiv` and `$HOME/.rhosts` files are documented in such resources as *TCP/IP Network Administration*, cited in *General TCP/IP Networking Resources* on page 39. Additional configuration information is provided in the `in.rlogind(8)` and `in.rshd(8)` man pages.

Since the trusted hosts files permit user login without a password, their use is strongly discouraged. If you configure trusted hosts in your network, then a compromise of one system will lead to a compromise of all systems that trust it. Hence, the r-commands are often referred to as the evil r-commands. All of the functionality of the r-commands can and should be securely replaced with SSH (discussed in Chapter 11).

## Some Major Applications

Throughout this book we will discuss the Network File System (NFS), Samba, the Network Information Services (NIS), and the Domain Name Service (DNS) as they relate to the various utilities we describe.

The NFS is a remote filesystem developed by Sun Microsystems, Inc. It allows for transparent local access to remote directories over TCP/IP. Unfortunately authentication has not been implemented for NFS in Linux as of the kernel version 2.2.x. Access control lists may be specified by the server in `/etc/exports`, and use by identified UID may be squashed (disallowed). You should always use access restrictions on every NFS resource. See the `exports(5)`, `nfs(5)`, and `mount(8)` man pages for more details. It is best from a security perspective to allow NFS access only within your organization's network and not to allow incoming NFS requests from the Internet (or other public network). This may be accomplished with `ipchains` (discussed in Chapter 16) or similar utility. For more information, additional references are cited at the end of this section.

Samba is conceptually similar to NFS except that it is implemented over the Microsoft Networking Protocol. Samba versions 1.9.17p2 and later are considered reasonably secure. Samba allows for password-based authentication and may be configured to pass hashed passwords instead of cleartext passwords over the network. It may also be configured with access control lists. Samba servers can be made to run in a chroot environment. Make sure that you take advantage of these security features.

NIS provides a mechanism to centrally administrate a collection of systems that are networked together. NIS was not designed with security in mind; rather it was designed for convenience. Do not allow access to your NIS database from networks other than those specifically involved in your NIS management. Implement access control through portmap (see Chapter 10).
