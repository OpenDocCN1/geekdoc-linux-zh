+   8. Check to see if two lines similar to the following are in the file and if not add them to the file or uncomment them:
+   
+       pop-3        110/tcp
+       pop-3        110/udp

+   9. Check to see if two lines similar to the following are in the file and if not add them to the file or uncomment them:
+   
+       imap2        143/tcp    imap
+       imap2        143/udp    imap

+   10. Save the file and close your text editor.

+   11. Force inetd to re-read its configuration file by sending it a SIGHUP signal:

```
# kill -HUP `cat /var/run/inetd.pid`
```

When you have enabled IMAP and POP3, you need to make sure that the services are responding to requests. You can do this by using Telnet to connect to the appropriate ports for each of the services.

To test POP3 on a host named somehost, Telnet to port 110 on somehost:

```
$ telnet somehost 110
Trying 10.20.30.40 ...
Connected to somehost.
Escape character is '^]'.
+OK POP3 somehost v7.59 server ready
^]telnet> q
```

To test IMAP on a host named somehost, Telnet to port 143 on somehost:

```
$ telnet somehost 143
Trying 10.20.30.40 ...
Connected to somehost.
Escape character is '^]'.
* OK somehost IMAP4rev1 v12.250 server ready
^]
telnet> q
```

If both tests succeed, your IMAP and POP3 servers are working and users with a login account on the server can use either protocol to access their mailboxes.

# USING PROCMAIL

As discussed earlier in this chapter, sendmail can use external mailers as mail delivery agents. One such external mailer is procmail, which is designed as a replacement for a local mailer.

Because procmail is generally considered to be roughly 30 percent faster than other local mailers and because it is also known to be extremely secure and stable, procmail is frequently used as the local mailer with sendmail.

procmail’s most important feature is that it provides a standard way to create rules (“recipes” in procmail terminology) for processing mail messages before they are added to a mailbox.