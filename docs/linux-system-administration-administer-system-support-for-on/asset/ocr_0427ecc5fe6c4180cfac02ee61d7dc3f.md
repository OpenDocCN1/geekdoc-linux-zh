What the Secure Shell programs do is create a random seed and enable login with a combination of a password and an RSA public-key pair. When the session is established, the information being passed between the Slackware host and the destination host is encrypted with DES, triple DES, IDEA, or other defined algorithms like Blowfish.

When the key is accepted, the slogin or ssh connection resembles something like a telnet or rlogin session. The encryption is transparent to the user, but someone sniffing network traffic will have a difficult time. Additionally, if compression is enabled, this will increase performance of the connection.

A secure shell session from my Slackware Linux system to my ISP account looks something like the following listing.

```
```
tigerden:/home/stripes- ssh tigerlair.com
stripes@tigerlair.com's password:
Last login: Mon Jul 20 01:00:34 1998 from dynamic22.pm04.m
Copyright (c) 1980, 1983, 1986, 1988, 1990, 1991, 1993, 1994
The Regents of the University of California.  All rights reserved.

Deleting old sig...
Picking new sig...
/home/stripes/.sigdir/sig.9

Mon Jul 20 01:17:59 PDT 1998
You have mail.
Experience is that marvelous thing that enables you to recognize a mistake
when you make it again.
- F. P. Jone
```
```

When I'm online, I don't have to worry about someone reading my typing or e-mail over the Internet without my permission. However, the Secure Shell program assumes that both hosts are trusted. If someone on my ISP were to root the system and break into my e-mail that way, I would not be protected through a cryptographic tunnel.

When I'm done, I log out as usual and the encrypted session ends:

```
```
tigerlair:~/user/home/stripes- exit
logout
Connection to tigerlair.com closed.
```
```