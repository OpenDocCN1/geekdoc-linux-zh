
250 2.1.0 Ok
RCPT TO: kyle@localhost
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: test
This is just a test
.
250 2.0.0 Ok: queued as 1ADD057CD0
quit
221 2.0.0 Bye
Connection closed by foreign host.

The first command you type is HELO followed by the name you want the system to know you as. Next type MAIL FROM: followed by the e-mail address you want the e-mail to appear to come from. After that type RCPT TO: followed by the e-mail address you want to send to. Then type DATA. At that point everything else you type will be considered the body of the e-mail. In my example I added a Subject: field but even that is optional. Just continue to type out your message and then when you are finished, enter then type a period, then type enter again. Finally type quit to end the session.

## Easy SSH Key Sharing

One of the annoying parts of setting up key authentication on SSH is having to move all the public keys around to each system’s authorized_keys file. For years I would do some fancy shell scripting to copy keys around, but then I found out that the openssh packages included a tool called ssh-copy-id just for that purpose. To use the program just type ssh-copy-id followed by the remote server (and optionally the remote username) you want the key copied to. For instance, if I wanted to copy my current user’s key to a server named web1, I could type:

```
$ ssh-copy-id web1
```

Or if I wanted to copy the key to the kyle user’s account on a server named db4, I would type:

```
$ ssh-copy-id kyle@db4
```

com.                 172800  IN  NS  J.GTLD-SERVERS.NET.
com.                 172800  IN  NS  A.GTLD-SERVERS.NET.
com.                 172800  IN  NS  M.GTLD-SERVERS.NET.
com.                 172800  IN  NS  G.GTLD-SERVERS.NET.
com.                 172800  IN  NS  E.GTLD-SERVERS.NET.
com.                 172800  IN  NS  I.GTLD-SERVERS.NET.
;; Received 504 bytes from 192.58.128.30#53(j.root-servers.net)
   in 110 ms

ubuntu.com.          172800  IN  NS  ns1.canonical.com.
ubuntu.com.          172800  IN  NS  ns2.canonical.com.
ubuntu.com.          172800  IN  NS  ns3.canonical.com.
;; Received 144 bytes from 192.41.162.30#53(L.GTLD-SERVERS.NET)
   in 91 ms

www.ubuntu.com.       600   IN  A   91.189.90.41
ubuntu.com.          172800  IN  NS  ns1.canonical.com.
ubuntu.com.          172800  IN  NS  ns2.canonical.com.
ubuntu.com.          172800  IN  NS  ns3.canonical.com.
;; Received 160 bytes from 91.189.94.173#53(ns1.canonical.com)
   in 151 ms

## Index

- \ (backslash)
- line continuation character, 93
- in sudoer aliases, 206
- % (percent sign)
- group name indicator, 204
- Kickstart section indicator, 106
- . (dot)
- alias for current directory, 20
- package paragraph separator, 62–63
- partition separator, 94, 96
- .. (dot dot), alias for directory above current, 20
- [ ] (square brackets)
- in grep search keywords, 477–478
- in regular expressions, 458
- @ (at sign), Kickstart task indicator, 106
- ^ (caret), Ctrl key symbol, 24
- # (hash mark), comment indicator
- source.list file, 72
- Upstart, 31
- < (left angle bracket), redirection operator, 462–464
- ? (question mark), wildcard character, 456
- > (right angle bracket), redirection operator, 462–464
- >> (right angle brackets), redirection operator, 462–464
- / (slash), in IRC commands, 444
- | (vertical line), pipe symbol, 458–459
- * (asterisk)
- in shell globs, 208–209, 457
- in traceroute output, 414
- wildcard character, 457
- ** (asterisks), in shell globs, 208–209
- 1n command
- hard links, creating, 468
- symlinks, creating, 467
- 450 command, 155
- 802.3ad or 4 mode, 366
- A
- A time, 12
- a2dissite script, 139
- a2ensite script, 138
- aa-complain program, 209
- aa-enforce program, 209
- abort command, 149
- Accessibility options, 4
- Account options, Kickstart, 109
- Active/active clusters, 369
- Active-backup or 1 mode, 365
- Active-backup policy, 365
- Active/passive clusters, 369
- Adaptive load balancing, 366
- Adaptive transmit load balancing, 366
- --add command, 346
- Administrator. See System administrator.
- Administrator (Windows). See Root user.
- Advanced Package Tools (APT). See APT (Advanced Package Tools).
- Alert escalations, 285–286
- Alerts for software upgrades, 64
- Aliases
- for directories, 20
- e-mail users, 147, 150
- nesting, 21
- newaliases command, 150
- sudo command, 205–206
- updating, 150
- allow command, 217
- Apache. See also Web servers.
- a2dissite script, 139
- a2ensite script, 138
