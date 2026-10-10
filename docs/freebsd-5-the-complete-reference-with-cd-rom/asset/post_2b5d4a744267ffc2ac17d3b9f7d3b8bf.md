
a sniffer on the sending, receiving, or sometimes even other local computers, the cracker can then record the password and use it to gain entry to the computer on which the server runs. If users employ the same passwords on multiple computers, the cracker can use one password to gain entry to many computers. Thus, unencrypted passwords are a serious problem. Whenever possible, you should use an encrypted password scheme, particularly if your local network wires are difficult to secure. SSH is a popular tool for encryption, and it encrypts *all* data it transfers, not just the password. As described in Chapter 21, SSH can be used in place of Telnet and FTP. With some more work, which is beyond the scope of this book for most protocols, SSH can be used to tunnel other protocols, lending its encryption advantages to almost any other protocol. Some protocols provide explicit support for encryption of passwords. Samba is one of these, but Samba’s encryption method requires it to use a non-PAM password database. VNC is another protocol that encrypts its passwords. Neither Samba nor VNC encrypts nonpassword data, though.

## Using Server-Specific Protections

Many servers, and especially many complex servers, provide protections that are unique to the servers themselves. You should consult the servers’ documentation for information on how to use such protections. Examples include:

- **IP address restrictions** Servers may allow or disallow connections from computers based on specific IP addresses. In fact, some servers, such as NFS and *rlogin*, use this method instead of usernames and passwords as the primary access-control method. Others use such protections as a *secondary security tool*. Some servers enable you to specify hostnames instead of or in addition to IP addresses, but doing so opens your system up to an indirect attack should your DNS server be compromised.

- **Network restrictions** You can often restrict access based on network addresses, much as you can restrict access based on IP addresses. Potentially more interesting, though, are restrictions based on network *interfaces*. For instance, you might set up an SSH server on a router so that you can administer the router; but to minimize abuse, you might configure SSH to respond to connection requests only from the network interface connected to the local network, not to the interface connected to the Internet.

- **Temporal restrictions** Some servers can be configured to accept accesses at some times of day but not at others. The *xinetd* (<http://www.xinetd.org>) super server, for instance, supports such restrictions. (*xinetd* can replace both *inetd* and TCP Wrappers.)

- **Local filesystem restrictions** Most file servers and login servers use the FreeBSD ownership and permissions system to restrict who may access what files. If the server requires a username and password, the user typically has the same permissions as when logged in at the console. (Some servers, though, such as Samba, provide overrides that can be quite complex.) Other servers run as a fixed user, and so provide access based on that account, not the ultimate user's login account.

- **“Strike-out” protections** Many servers disconnect from the client or take special actions after some number of authentication errors or suspicious commands. For instance, some mail servers impose increasing delays whenever a sender tries to send to an unauthorized address. This measure helps make your system unappealing to would-be spammers.

- **Remote username logging** Most servers log some of their activities to /var/log/messages or other log files. Some servers can be configured to include information on the client's username, if the remote system is running an ident (aka auth) server. This information doesn't directly protect the server or your system, but it may be useful in tracking abuse. If you have this information in your log and contact the remote system's administrator, that administrator can more easily track the abusive individual and take appropriate action.

Some of these features can be added with tools outside of the server. For instance, you could use cron jobs (described in Chapter 6) to alter a system's firewall rules (described in Chapter 17) so as to enable or disable access to specific ports at specific times, creating temporal restrictions even for servers that don't normally support this feature. Firewall rules alone can impose restrictions based on IP addresses.

## Using TCP Wrappers

TCP Wrappers is a standard security tool in UNIX and UNIX-like OSes, including FreeBSD. TCP Wrappers is an access-control tool. It's most commonly called by the inetd super server as a preliminary step in launching a server in response to a connection request. For instance, suppose a computer is running an FTP server via inetd, and an FTP connection request comes in. inetd answers this request, but immediately hands it off to TCP Wrappers, which examines the nature of the request—most importantly, the originating IP address. If this address meets the criteria in TCP Wrappers' configuration file, the program then launches the FTP server and tells it to handle the request. Ordinarily, all of this takes a fraction of a second, so it's not noticeable to the person using the client. If the incoming request doesn't match TCP Wrappers' criteria, the connection can be terminated before it's passed on to the target server.

Using TCP Wrappers enables you to apply consistent access controls to all the servers mediated by inetd. (Some servers also call TCP Wrappers directly, and so can be protected by TCP Wrappers even if the server isn't launched by inetd.) You can also configure TCP Wrappers to apply different criteria to different servers. This combination means that servers intended to be launched from inetd can simplify themselves by omitting code to explicitly support features such as restrictions based on IP addresses because TCP Wrappers handles the job.

When you launch **inetd** with the `-w` or `-W` option, it automatically uses TCP Wrappers for internal (inetd-provided) or external services, respectively. The default startup method for **inetd** uses both of these options, so unless you reconfigure it, FreeBSD uses TCP Wrappers for all **inetd**-mediated servers by default. You can verify that this is the case by typing the following command:

```
$ ps ax | grep inetd

183 ?? Is 0:00.10 /usr/sbin/inetd -wW
```

This command shows the **inetd** process, including the `-wW` options. If you don't see these options, or don't see an **inetd** process at all, consult Chapter 16 for more information on starting and using **inetd**.

The /etc/hosts.allow file controls TCP Wrappers. Like many configuration files, this file uses a pound sign (#) as a comment indicator. Other lines take the following format:

```
daemon-list : client-list : option [: option ...]
```

> Some early versions of FreeBSD and some non-FreeBSD systems use two files to control TCP Wrappers, *hosts.allow* and *hosts.deny*. The method described here adds the specification of whether to allow or deny access to the single configuration file. Earlier systems left this information in the name of the file.

The elements in each control line have specific meanings:

- **daemon-list** The *daemon-list* is a list of one or more servers. You can specify the servers by their names in /etc/services or by various keywords, such as *ALL* (which matches all servers). TCP Wrappers also accepts the names of certain specific servers, such as *sendmail*. When listing multiple servers, separate their names by commas or spaces.

- **client-list** The *client-list* is a list of one or more clients. You can specify clients by hostname, IP address, patterns, or wildcards, as described shortly. As with *daemon-list*, you can specify several clients separated by commas or spaces, and certain keywords apply, including *ALL* to match any client.

- **option** In most cases, *option* will be allow or deny to grant or block access, respectively. It's possible to provide several colon-separated *option* fields, though, in which case options before the final one specify extra commands to be run or tests to be performed. Such advanced configurations are beyond the scope of this chapter.

Both the *daemon-list* and the *client-list* support the *EXCEPT* keyword, which enables you to specify an exception to some other rule. For instance, a *daemon-list* of *ALL EXCEPT telnet* creates a rule that applies to all protected
