
you would change it to the following to use TCP wrappers:

```
ftp     stream    tcp     nowait    root    /usr/sbin/tcpd   in.ftpd
    -l -a
```

The normal daemon server path is replaced with the path for tcpd, with the argument being the actual server to run. TCP wrappers uses two files to configure allowed connections:

- /etc/hosts.allow
- /etc/hosts.deny

Both configuration files use the same format. If either file does not exist, it is considered to be empty. If there are entries in hosts.allow, but not hosts.deny, anything not explicitly granted is denied. Conversely, if there are entries in hosts.deny, but not in hosts.allow, connections are allowed unless explicitly denied. If entries exist in both, the hosts.allow is checked first, and then hosts.deny. So even if a connection is denied in hosts.deny, it can be overridden with hosts.allow. The syntax for these files is as follows:

```
service: host_list [: shell command]
```

The service name is exactly the name listed in /etc/services and /etc/inetd.conf. The host list is a list of hosts, domains, wildcards, or CIDR addresses. For example, the following entry in /etc/hosts.allow would allow any host in the nashes.net domain to connect to the FTP server:

```
in.ftpd: .the-nashes.net
```

Table 17-1 shows the possible host and service match methods.

### Table 17-1 Match Methods

| Method | Function |
| :--- | :--- |
| .domain.org | A domain that begins with a dot means "any host in that domain." |
| 192.168. | Any numeric address that ends in a dot means any host that has that IP prefix. This would match 192.168*. |
| Address/Mask | A combination of a network address and subnet mask, such as 192.168.0.0/16. |
| ALL | Match any client or service name. |
| LOCAL | Match any client hostname that does not contain a dot. |
| EXCEPT | Allows exceptions to ALL. |

> **Caution** Be careful with the `LOCAL` command. If your `/etc/hosts` file contains an entry with just a host name and no domain, it may be *allowed* access whether it is actually local or not.

The optional shell command can be used to perform a function when a client connects that matches the specified rule. A number of patterns can be used in the shell command that are expanded out when run. Table 17-2 lists these patterns. Another useful option is the `twist` command. This causes the output of the shell command to be shown to the connecting client, along with any information from the expansion patterns. For example:

```
in.telnetd : .evil.org : twist /bin/echo "Sorry &c, but we don't want your kind around here."
```

This would cause the message to be echoed out to any user from the `evil.org` domain connecting to the Telnet server.

**Table 17-2 tcpd Patterns**

| Pattern | Function |
| :--- | :--- |
| %a | The connecting client's host address. |
| %A | The server's host address. |
| %c | Client information such as user@host, user@address, hostname, or address depending on what is available. |
| %d | The daemon process name. |
| %h | The connecting client's hostname, or address if the host cannot be retrieved. |
| %H | The server's hostname, or address if the host cannot be retrieved. |
| %n | The client hostname. |
| %N | The server hostname. |
| %p | The daemon's process ID. |
| %s | Server information such as daemon@host, daemon@address, or just the daemon name depending on what is available. |
| %u | The client user name, or unknown. |

TCP wrappers provide a couple of utilities to check your configuration. The first is `tcpdchk`. It is used to check your syntax and make sure the rules do what you are expecting. Table 17-3 lists the `tcpdchk` command-line options. The following is sample output from `tcpdchk`.

```
Using network configuration file: /etc/inetd.conf
>>> Rule /etc/hosts.allow line 7:
daemons: in.ftpd
clients: .the-nashes.net
access: granted

>>> Rule /etc/hosts.deny line 9:
daemons: ALL
clients: ALL
access: denied
```

**Table 17-3 tcpdchk Options**

| Option | Function |
| :--- | :--- |
| -a | Report rules that allow access without an explicit ALLOW statement. |
| -d | Check the hosts.allow and hosts.deny files in the current directory instead of those in /etc. |
| -i inetd_conf | Path to your inetd.conf file, if not using the current one in /etc. |
| -v | Display all access control rules. By default no output is displayed if no problems are found. |

Another tool provided is tcpdmatch. The syntax is as follows:

```
tcpdmatch [-d] [-i inet_conf] daemon client
```

The -d and -i options are the same as with tcpdchk. The tcpdmatch tool allows you to provide theoretical connections to your system and watch your results. For example, using the rules:

```
hosts.deny
ALL      :   ALL

hosts.allow
in.ftpd  :   .the-nashes.net
```

testing a connection from norbert.the-nashes.net to the FTP and Telnet servers would produce the following:

```
[root@redhat /etc]# /usr/sbin/tcpdmatch in.ftpd
jason@norbert.the-nashes.net
client:  hostname norbert.the-nashes.net
client:  address   216.254.90.133
client:  username jason

server: process in.ftpd
matched: /etc/hosts.allow line 7
access: granted

[root@redhat /etc]# /usr/sbin/tcpdmatch in.telnetd
jason@norbert.the-nashes.net
client: hostname norbert.the-nashes.net
client: address 216.254.90.133
client: username jason
server: process in.telnetd
matched: /etc/hosts.deny line 9
access: denied
```

![](img/96d9ccd181675a8ae8b6a1146c919d2b_733_0.png)

> TCP wrappers cannot be used with applications that use the UDP.

# SUID security issues

Applications that are set as SUID root can be used to gain root access to the system. Only applications that require SUID should be set so. If the application does not have to run as root, you can create a separate account for just that application and assign rights only where needed. This way if someone uses the application to gain access to the system, they have only the account’s permissions and cannot do harm to the rest of the system.

It is useful to occasionally check to see which files are SUID on the system. It is an even better idea to set up a *cron job* to do this periodically and have it mail you the results. The following command would accomplish this:

```
/usr/bin/find / -user root -perm -4000 -print | /bin/mail -s "Files that are SUID root" <mail address>
```

If you know that a file system has no applications that need to be SUID, consider mounting it with the `-o nosuid` option. This way an application cannot be accidentally installed SUID without your knowledge.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_733_1.png)

Some systems automatically remove the SUID status of a shell script when it is run to reduce the security risk.

# Managing packages

Many administrators and users now download precompiled binary packages for software. Downloading these packages is much more convenient than downloading source code and having to compile it. The problem is that unlike source code, which can be manually verified for backdoors or other security problems, binary files must be taken as is. To minimize this risk, you should get binary packages only from the creator’s Web site and check them for validity.

RPM includes functions to let you check the integrity of a package to make sure it was downloaded correctly and not tampered with. The -K or --checksig option validates the integrity of a package using MD5 or GnuPG.

```
rpm -K package_file.rpm
```

For this to work the following steps must be taken:

1. Install the GnuPG application, available from http://www.gnupg.org.
2. Add the public key for the appropriate package maintainers to your key ring using the gpg -import command.

If the package validates correctly, rpm will output a message similar to the following:

```
[root@redhat /root]# rpm -K wget-1.5.3-6.src.rpm
wget-1.5.3-6.src.rpm: md5 gpg OK
```

Debian does not offer such an integrated approach. The usual method is to use the md5sum tool and compare its output to a published value. If the value matches, the software is most likely not compromised.

# Using setgid

Changing a file to be setgid causes it to run with the group's permissions, but this setting has a different meaning with directories. Normally, when a user creates a file in a directory, the group owner of the file is set to that of the user. When setgid, or SGID, is set on the directory, the file has the group owner of the directory, not the user.

> Exam Tip: The SGID bit is used to create a shared directory.

Red Hat uses this plus a umask of 002 to allow you to create directories to share files. Normally, the umask is set to 022 on most Linux distributions. With a umask of 022, the permissions for a new file are 755, so the group does not have write access. If a new file is created in a directory that is setgid, the group owner is that of the directory, but members of the group still cannot write to the file. Red Hat gets around this with its umask of 002. Newly created files have the group owner of the directory, and 775 permissions.

This is useful when making a directory to hold shared files. Just add all of the users who need to access the files to a group that also owns the shared directory and set the directory setgid.
