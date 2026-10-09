
## SENDING MAIL TO A REMOTE USER

Given a user's username on a remote system and the name of the remote system or its domain, you can use an email program to send a message over the network or the Internet, using the `@` form of an address:

zach@bravo

*or*

zach@example.com

Although many Linux utilities recognize the `@` form of a network address, you may find that you can reach more remote computers with email than with the other networking utilities described in this chapter. This disparity arises because the email system can deliver a message to a host that does not run IP, even though it appears to have an Internet address. The message may be routed over the network, for example, until it reaches a remote system that has a point-to-point, dial-up connection to the destination system. Other utilities, such as talk, rely on IP and operate only between networked hosts.

## MAILING LIST SERVERS

A mailing list server (listserv¹⁴) allows you to create and manage an email list. An electronic mailing list provides a means for people interested in a particular topic to participate in an electronic discussion and for a person to disseminate information periodically to a potentially large mailing list. One of the most powerful features of most list servers is their ability to archive email postings to the list, create an archive index, and allow users to retrieve postings from the archive based on keywords or discussion threads. Typically you can subscribe and unsubscribe from the list with or without human intervention. The owner of the list can restrict who can subscribe, unsubscribe, and post messages to the list. See page 734 for instructions on configuring the Mailman list server. Other popular list servers include LISTSERV (www.lsoft.com), Lyris (www.lyris.com), and Majordomo (www.greatcircle.com/majordomo). Ubuntu maintains quite a few mailing lists and list archives for those mailing lists at lists.ubuntu.com. Use Google to search on linux mailing list to find other lists.

¹⁴ Although the term listserv is sometimes used generically to include many different list server programs, it is a specific product and a registered trademark of L-soft International, Inc.: LISTSERV (for more information go to www.lsoft.com).

## NETWORK UTILITIES

To realize the full benefits of a networked environment, it made sense to extend certain tools, some of which have already been described. The advent of networks also created a need for new utilities to control and monitor them, spurring the development of new tools that took advantage of network speed and connectivity. This section describes concepts and utilities for systems attached to a network.

## TRUSTED HOSTS

Some commands, such as rep and rsh, work only if the remote system trusts your local computer (that is, if the remote system knows your local computer and believes that it is not pretending to be another system). The /etc/hosts.equiv file lists trusted systems. For reasons of security, the root account does not rely on this file to identify trusted privileged users from other systems.

Host-based trust is largely obsolete. Because there are many ways to circumvent trusted host security, including subverting DNS systems and IP spoofing (page 1154), authentication based on IP address is widely regarded as insecure and obsolete. In a small homogeneous network of machines with local DNS control, it can be “good enough.” Its greater ease of use in these situations may outweigh the security concerns.

### Do not share your login account

You can use a ~/.rhosts file to allow another user to log in as you from a remote system without knowing your password. This setup is not recommended. Do not compromise the security of your files or the entire system by sharing your login account. Use ssh and scp instead of rsh and rcp whenever possible.

## OPENSSH TOOLS

The OpenSSH project provides a set of tools that replace rcp, rsh, and others with secure equivalents. These tools are installed by default in Ubuntu Linux and can be used as drop-in replacements for their insecure counterparts. The OpenSSH tool suite is covered in detail in Chapter 18.

## telnet: LOGS IN ON A REMOTE SYSTEM

You can use the TELNET protocol to interact with a remote computer. The telnet utility, a user interface to this protocol, is older than ssh and is not secure. Nevertheless, it may work where ssh (page 670) is not available (there is more non-UNIX support for TELNET access than for ssh access). In addition, many legacy devices, such as terminal servers and network devices, do not support ssh.

```
[bravo]$ telnet kudos
Trying 172.19.52.2..
Connected to kudos.example.com
Escape character is '^]' 

Welcome to SuSE Linux 7.3 (i386) - Kernel 2.4.10-4GB (2).
kudos login: wild
Password:
You have old mail in /var/mail/wild.
Last login: Mon Feb 27 14:46:55 from bravo.example.com
wild@kudos:~>
..
.
wild@kudos:~> logout
Connection closed by foreign host.
[bravo]$
```

### telnet versus ssh

When you connect to a remote UNIX or Linux system using telnet, you are presented with a regular, textual login: prompt. Unless you specify differently, the ssh utility assumes that your username on the remote system matches that on the local system. Because telnet is designed to work with non-UNIX and non-Linux systems, it makes no such assumptions.

### telnet is not secure

> Whenever you enter sensitive information, such as your password, while you are using telnet, it is transmitted in cleartext and can be read by someone who is listening in on the session.

Another difference between these two utilities is that telnet allows you to configure many special parameters, such as how RETURNs or interrupts are processed. When using telnet between UNIX and/or Linux systems, you rarely need to change any parameters.

When you do not specify the name of a remote host on the command line, telnet runs in an interactive mode. The following example is equivalent to the previous telnet example:

```
[bravo]$ telnet
 telnet> open kudos
  Trying 172.19.52.2..
  Connected to kudos.example.com
  Escape character is '^]' 
  ..
```

Before connecting you to a remote system, telnet tells you what the *escape character* is; in most cases, it is `^]` (where `^` represents the CONTROL key). When you press CONTROL-], you escape to telnet's interactive mode. Continuing the preceding example:

```
[kudos]$ CONTROL-]
 telnet> ?

 (displays help information)

 telnet> close
  Connection closed.
 [bravo]$
```

When you enter a question mark in response to the telnet> prompt, telnet lists its commands. The close command ends the current telnet session, returning you to the local system. To get out of telnet's interactive mode and resume communication with the remote system, press RETURN in response to a prompt.

You can use telnet to access special remote services at sites that have chosen to make such services available. However, many of these services, such as the U.S. Library of Congress Information System (LOCIS), have moved to the Web. As a consequence, you can now obtain the same information using a Web browser.

### Using telnet to connect to Other Ports

By default telnet connects to port 23, which is used for remote logins. However, you can use telnet to connect to other services by specifying a port number. In addition to standard services, many of the special remote services available on the Internet use unallocated port numbers. For example, you can access some multiplayer text games, called MUDs (Multi-User Dungeons, or Dimensions), using telnet to connect to a specified port, such as 4000 or 8888. Unlike the port numbers for standard protocols, these port numbers can be picked arbitrarily by the administrator of the game.

While telnet is no longer commonly employed to log in on remote systems, it is still used extensively as a debugging tool. This utility allows you to communicate directly with a TCP server. Some standard protocols are simple enough that an experienced user can debug problems by connecting to a remote service directly using telnet. If you are having a problem with a network server, a good first step is to try to connect to it using telnet.

In the following example, a system administrator who is debugging a problem with email delivery uses telnet to connect to the SMTP port (port 25) on the server at example.com to see why it is bouncing mail from the spammer.com domain. The first line of output indicates which IP address telnet is trying to connect to. After telnet displays the Connected to smtprv.example.com message, the user emulates an SMTP dialog, following the standard SMTP protocol. The first line, which starts with helo, begins the session and identifies the local system. After the SMTP server responds, the user enters a line that identifies the mail sender as user@spammer.com. The SMTP server's response explains why the message is bouncing, so the user ends the session with quit.

```
$ telnet smtprv 25
Trying 192.168.1.1...
Connected to smtprv.example.com.
Escape character is '^]' .
helo example.com
220 smtprv.example.com ESMTP Sendmail 8.13.1/8.13.1; Wed, 4 May 2005 00:13:43 -0500 (CDT)
250 smtprv.example.com Hello desktop.example.com [192.168.1.97], pleased to meet you
mail from: user@spammer.com
571 5.0.0 Domain banned for spamming
quit
221 2.0.0 smtprv.example.com closing connection
```

The telnet utility allows you to use any protocol you want, as long as you know it well enough to type commands manually.

## ftp: TRANSFERS FILES OVER A NETWORK

The File Transfer Protocol (FTP) is a method of downloading files from and uploading files to another system using TCP/IP over a network. FTP is not a secure protocol; use it only for downloading public information from a public server. Most Web browsers can download files from FTP servers. Chapter 19 covers FTP clients and servers.

## ping: TESTS A NETWORK CONNECTION

The ping¹⁵ utility (http://ftp.arl.mil/~mike/ping.html) sends an ECHO REQUEST packet to a remote computer. This packet causes the remote system to send back a

¹⁵. The name ping mimics the sound of a sonar burst used by submarines to identify and communicate with each other. The word ping also expands to packet internet groper.
