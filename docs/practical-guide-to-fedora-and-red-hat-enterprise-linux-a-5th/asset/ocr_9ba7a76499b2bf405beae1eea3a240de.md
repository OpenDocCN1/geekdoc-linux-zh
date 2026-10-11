for standard protocols, these port numbers can be picked arbitrarily by the admin-\nistrator of the game.

While **telnet** is no longer commonly employed to log in on remote systems, it is still\nused extensively as a debugging tool. This utility allows you to communicate\ndirectly with a TCP server. Some standard protocols are simple enough that an\nexperienced user can debug problems by connecting to a remote service directly\nusing **telnet**. If you are having a problem with a network server, a good first step is\nto try to connect to it using **telnet**.

In the following example, a system administrator who is debugging a problem with\nemail delivery uses **telnet** to connect to the SMTP port (port 25) on a the server at\n**example.com** to see why it is bouncing mail from the **spammer.com** domain. The\nfirst line of output indicates which IP address **telnet** is trying to connect to. After **tel**-\nnet displays the **Connected to smtpsrv.example.com** message, the user emulates an\nSMTP dialog, following the standard SMTP protocol. The first line, which starts\nwith **helo**, begins the session and identifies the local system. After the SMTP server\nresponds, the user enters a line that identifies the mail sender as **user@spammer.com** .\nThe SMTP server's response explains why the message is bouncing, so the user ends\nthe session with **quit** .

```
```
$ telnet smtpsrv 25
Trying 192.168.1.1...\nConnected to smtpsrv.example.com.\nEscape character is '^]'.\n\n220 smtpsrv.example.com ESPMTP Sendmail 8.13.1/8.13.1; Sun, 4 May 2008 00:13:43 -0500 (CDT)\n250 smtpsrv.example.com Hello desktop.example.com [192.168.1.97], pleased to meet you\n550 from:user@spammer.com\n571 5.0.0 Domain banned for spamming\nquit\n221 2.0.0 smtpsrv.example.com closing connection\n```

```

The telnet utility allows you to use any protocol you want, as long as you know it\nwell enough to type commands manually.

# ## ftp: **TRANSFERS FILES OVER A NETWORK**

The File Transfer Protocol (FTP) is a method of downloading files from and uploading\nfiles to another system using TCP/IP over a network. FTP is not a secure protocol; use\nit only for downloading public information from a public server. Most Web browsers\ncan download files from FTP servers. Chapter 19 covers FTP clients and servers.

# ## ping: **TESTS A NETWORK CONNECTION**

The **ping** 15 utility (http://ftp.arl.mill-mike//ping.html) sends an ECHO_REQUEST\npacket to a remote computer. This packet causes the remote system to send back a

15. The name **ping** mimics the sound of a sonar burst used by submarines to identify and communicate with each\nother. The word **ping** also expands to packet internet groper.