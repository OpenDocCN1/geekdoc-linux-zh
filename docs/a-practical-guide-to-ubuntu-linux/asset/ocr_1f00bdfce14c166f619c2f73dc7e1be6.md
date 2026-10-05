# NETWORK UTILITIES 393

called MUDs (Multi-User Dungeons, or Dimensions), using telnet to connect to a specified port, such as 4000 or 8888. Unlike the port numbers for standard protocols, these port numbers can be picked arbitrarily by the administrator of the game.

telnet is no longer commonly employed to log in on remote systems, it is still used extensively as a debugging tool. This utility allows you to communicate directly with a TCP server. Some standard protocols are simple enough that an experienced user can debug problems by connecting to a remote service using telnet. If you are having a problem with a network server, a first step is to connect to it using telnet.

In the following example, a system administrator who is debugging a problem with email delivery uses telnet to connect to the SMTP port (port 25) on the server at example.com to see why it is bouncing mail from the spammer domain. The first line of output shows which IP address telnet is trying to connect to. After telnet displays the Connected to smpsrv.example.com message, the user employs an SMTP dialog, following the standard SMTP protocol. The first line, which starts with hello, begins the session and identifies the local system. After the SMTP server's response explains why the message is bouncing, so the user ends with quit.

```
$ telnet smpsrv.168.1....
Trying 192.168.1.
Connected to smpsrv.example.com.
Escape character is '^A'.
hello example.com
220 smpsrv.example.com SMTP Sendmail 8.13.1/8.13.1; Wed, 4 May 2005 00:13:43 -0500 (CDT)
250 smpsrv.example.com Hello desktop [192.168.1.97], pleased to meet you
mail from:user@spam.com
```

+   571 5.0.0 Domain banned for spamming
quit
221 2.0.0 smpsrv.example.com connection closing

The telnet utility allows you to use any protocol, as long as you know it well enough to type commands manually.

# ftp: TRANSFERS FILES OVER A NETWORK

The File Transfer Protocol (FTP) is a method of downloading files from uploading files to another system using TCP/IP over a network. FTP is not a secure protocol; use it only for downloading public information from a public server. Web browsers can download files from FTP servers. Chapter 19 covers FTP clients and servers.

# ping: TESTS A NETWORK CONNECTION

The ping15 utility (http://ftp.arl.ml/~mike/ping.html) sends an ECHO_REQUEST packet to a remote computer. This packet causes the remote system to send back a

> 15. The name ping mimics the sound of a sonar by submarines to identify and communicate with each other. The word ping also expands to packet internet grep.