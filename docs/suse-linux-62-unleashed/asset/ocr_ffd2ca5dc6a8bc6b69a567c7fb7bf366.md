```
root@gonzo /] /etc/rc.d.init/inet stop
root@gonzo /] /etc/rc.d.init/inet start
```

By now, imap is running and you should be able to connect to it. This is similar to the way you tested the connection to your POP server in the previous section.

Type in

```
telnet imapserver imap
```

where imapserver is the name of the machine running the imapd program. You should get a response similar to the following:

+   * OK imapserver IMAPrev1 v12.250 server ready

This means the IMAP server has responded and is awaiting an instruction (again, this is normally done by the client mail reader). If you want to test the authentication service, try to log in as yourself and see whether the service registers your current email box. For example, to log in as ssh with the password mars1031, enter

```
A001 user ssh mars1031
A001 OK LOGIN completed
```

You are now logged into your IMAP server. Since you were just testing, you can log out now by entering

```
A002 logout
```

+   * BYE imapserver IMAPrev1 server terminating connection

Your IMAP server is set up and ready to use!

# Mail Retrieval

With imapset on your server, you can access your mail using numerous methods. You can use a command-line program such as pine on the Linux console, an IMAP-compliant Windows or Macintosh-based email client (a list of which can be found at http://www.imap.org/products.html), or Netscape Communicator, which is available as part of the SuSE Linux distribution.

# Configuring Netscape for POP3 or IMAP Retrieval

It's fairly simple to set up Netscape to talk to your mail server. You just need to tell your IMAP or POP server name, your login name, and if you want to use IMAP, the subdirectory in your home directory on the server where your folders are kept.