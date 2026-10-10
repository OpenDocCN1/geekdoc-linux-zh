candidates are services such as: shell, login, exec, uucp, ftp, and informational services such as finger, netstat, and systat.

There are all sorts of security and access control mechanisms. I’ll describe the most elementary of them.

# ## /etc/ftpusers

The /etc/ftpusers file is a simple mechanism that allows you to deny certain users from logging into your machine via ftp. The /etc/ftpusers file is read by the ftp daemon program (ftpd) when an incoming ftp connection is received. The file is a simple list of those users who are disallowed from logging in. It might looks something like:

```
```
# /etc/ftpusers - users not allowed to login via ftp
root
uucp
bin
mail
```
```

# ## /etc/securetty

The /etc/securetty file allows you to specify which tty devices root is allowed to login on. The /etc/securetty file is read by the login program (usually /bin/login). Its format is a list of the tty devices names allowed; on all others root login is disallowed:

```
```
# /etc/securetty - tty's on which root is allowed to login
tty1
tty2
tty3
tty4
```
```

# ## The Tcpd Hosts Access Control Mechanism

The tcpd program you will have seen listed in the same /etc/inetd.conf provides logging and access control mechanisms to services it is configured to protect.

When it is invoked by the inetd, orienetd, it reads two files containing access rules and either allows or denies access to the server it is protecting, accordingly.

It will search the rules files until the first match is found. If no match is found, then it assumes that access should be allowed to anyone. The files