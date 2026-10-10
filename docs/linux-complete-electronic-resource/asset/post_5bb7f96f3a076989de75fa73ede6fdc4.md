
## Chapter 9
### PPP

This document shows how to connect your Linux PC to a PPP server, how to use PPP to link two LANs together, and it provides one method of setting up your Linux computer as a PPP server. The document also provides help in debugging nonfunctional PPP connections.

If your Internet Service Provider is telephone-line and modem-based, then they are almost certainly providing you with PPP service. You'll definitely want to read this chapter to learn all about how PPP works under Linux. In some cases, it'll be a little tricky to get going, but everything you need to know should be here, and you'll only have to do it once, so don't give up!

*PPP* is reprinted from the Linux PPP HOWTO by Robert Hart, version 3 of 31 March 1997.

### Copyright

This document is distributed under the terms of the GPL (GNU Public License).

### Distribution

This document will be posted to `comp.os.linux.answers` as new versions of the document are produced. It is also available in HTML format at

- Linux HOWTO Index (see `http://MetaLab.unc.edu/mdw/Linux.html#howto`)
- PPP-HOWTO (see `http://www.interwft.com.au/other/ppp-HOWTO/ppp-howto.html`)

Other formats (SGML, ASCII, PostScript, DVI) are available from “HOWTOs–other formats” (see `ftp://MetaLab.unc.edu/pub/Linux/docs/HOWTO/other-formats`).

As MetaLab.unc.edu carries a very heavy load, please use an appropriate mirror site close to you.

### Acknowledgements

A growing number of people have provided me with assistance in preparing this document. Special thanks go to Al Longyear for the guidance on PPP itself (if there are mistakes here, they are mine not his), Greg Hankins (maintainer of the Linux Howto system), and Debi Tackett (of MaximumAccess.com) for many helpful suggestions on style, content order, logic, and clarity of explanations.

Finally, to the many people who have contacted me by e-mail offering comments—my thanks. As with all HOWTO authors, the satisfaction of helping is all the payment we receive and it is enough. By writing this HOWTO I am repaying in a small way the debt I—and all other Linux users—owe to the people who write and maintain our OS of choice.

### INTRODUCTION

PPP (The Point to Point Protocol) is a mechanism for creating and running IP (the Internet Protocol) and other network protocols over a serial link—be that a direct serial connection (using a null-modem cable), over a telnet established link, or a link made using modems and telephone lines (and of course using digital lines such as ISDN).

Using PPP, you can connect your Linux PC to a PPP server and access the resources of the network to which the server is connected (almost) as if you were directly connected to that network.

You can also set up your Linux PC as a PPP server, so that other computers can dial into your computer and access the resources on your local PC and/or network.

As PPP is a peer-to-peer system, you can also use PPP on two Linux PCs to link together two networks (or a local network to the Internet), creating a Wide Area Network (WAN).

One major difference between PPP and an Ethernet connection is, of course, speed-a standard Ethernet connection operates at 10 Mbs (Megabits [million bits] per second) maximum theoretical throughput, whereas an analogue modem operates at speeds up to 56 kbps (kilobits [thousand bits] per second).

Also, depending on the type of PPP connection, there may be some limitations in usage of some applications and services.

### Clients and Servers

PPP is strictly a peer-to-peer protocol; there is (technically) no difference between the machine that dials in and the machine that is dialed into. However, for clarity's sake, it is useful to think in terms of servers and clients.

When you dial into a site to establish a PPP connection, you are a client. The machine to which you connect is the server.

When you are setting up a Linux box to receive and handle dial-in PPP connections, you are setting up a PPP server.

Any Linux box can be both a PPP server and client-even simultaneously if you have more than one serial port (and modem if necessary). As stated above, there is no real difference between clients and servers as far as PPP is concerned, once the connection is made.

This document refers to the machine that initiates the call (that dials in) as the client, while the machine that answers the telephone, checks the authentication of the dial-in request (using user names, passwords, and possibly other mechanisms) is referred to as the server.

The use of PPP as a client to link one or more machines at a location into the Internet is, probably, the one in which most people are interested-that is using their Linux box as a client.

The procedure described in this document will allow you to establish and automate your Internet connection.

This document will also give you guidance in setting up your Linux PC as a PPP *server* and in linking two LANs together (with full routing) using PPP. (This is frequently characterized as establishing a WAN [wide area network] link.)

## Differences between Linux Distributions

There are many different Linux distributions and they all have their own idiosyncrasies and ways of doing things.

In particular, there are two different ways a Linux (and Unix) computer actually starts up, configures its interfaces, and so forth.

These two ways are *BSD system initialization* and *System V system initialization*. If you dip into some of the Unix news groups, you will find occasional religious wars between proponents of these two systems. If that sort of thing amuses you, have fun burning bandwidth and join in!

Possibly the most widely used distributions are:

- *Slackware*, which uses BSD style system initialization
- *Red Hat* (and its former associate, Caldera), which use SysV system initialization (although in a slightly modified form)
- *Debian*, which uses SysV system initialization

BSD style initialization typically keeps its initialization files in */etc*/. . . These files are

```
/etc/rc
/etc/rc.local
/etc/rc.serial
(and possibly other files)
```

Of recent times, some BSD system initialization schemes use a */etc/rc.d*. . . directory to hold the startup file rather than putting everything into */etc*.

System V initialization keeps its initialization files in directories under */etc*/. . . or */etc/rc.d*/. . . and a number of subdirectories under there:

```
drwxr-x-x  2 root    root    1024 Jul  6 15:12 init.d
-rwxr-x-x  1 root    root     1776 Feb  9  05:01 rc
-rwxr-x-x  1 root    root      820 Jan  2  1996 rc.local
-rwxr-x-x  1 root    root     2567 Feb  5  20:30 rc.sysinit
drwxr-x-x  2 root    root     1024 Jul  6  15:12 rc0.d
drwxr-x-x  2 root    root     1024 Jul  6  15:12 rc1.d
drwxr-x-x  2 root    root     1024 Jul  6  15:12 rc2.d
drwxr-xr-x  2 root    root     1024 Jul 18  18:07 rc3.d
drwxr-xr-x  2 root    root     1024 May 27  1995 rc4.d
drwxr-xr-x  2 root    root     1024 Jul  6  15:12 rc5.d
drwxr-xr-x  2 root    root     1024 Jul  6  15:12 rc6.d
```

If you are trying to track down where your Ethernet interface and associated network routes are actually configured, you will need to track through these files to find where the commands are that do this.

## Distribution-Specific PPP Configuration Tools

On some installations (for example Red Hat and Caldera), there is a X Windows configured PPP dial-up system. This HOWTO does not cover these distribution-specific tools. If you are having problems with them, contact the distributors directly.

For Red Hat 4.x users, there is now a Red Hat PPP-TIP (see http://www.interweft.com.au) in the Linux resources area and also from Red Hat Software (see http://www.redhat.com) in the support area.

## IP NUMBERS

Every device that connects to the Internet must have its own, unique IP number. These are assigned centrally by a designated authority for each country.

If you are connecting a local area network (LAN) to the Internet, you must use an IP number from your own assigned network range for all the computers and devices you have on your LAN. You must not pick IP numbers out of the air and use these while connecting to another LAN (let alone the Internet). At worst this will simply not work at all and could cause total havoc as your "stolen" IP number starts interfering with the communications of another computer that is already using the IP number you have picked out of the air.

Please note that the IP numbers used throughout this document (with some exceptions) are from the "unconnected network numbers" series that are reserved for use by networks that are not (ever) connected to the Internet.

There are IP numbers that are specifically dedicated to LANs that do not connect to the Internet. The IP number sequences are

- One A Class Network Address 10.0.0.0 (netmask 255.0.0.0)

![](img/a3584dae761d2e3abed8bf40d7637389_314_0.png)
