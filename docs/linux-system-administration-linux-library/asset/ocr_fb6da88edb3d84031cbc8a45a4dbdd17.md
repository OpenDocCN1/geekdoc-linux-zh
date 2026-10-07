News servers The Network News Transport Protocol (NNTP) controls the trans-
fer Usenet news—a global discussion forum in which users post queries, solutions,
of other discussions of topics as vegetarian cooking, Linux, and the Inter-
national Space Station. News servers typically exist at ISPs and for large organizations,
as universities. They exchange articles with each other, resulting in the global
span Usenet news. You can run a news server yourself, either if you're in charge
of the news server for a large organization or if you want to run a small news server
for internal use or to maintain local copies of the newsgroups in which you're-ested. Red Hat Linux connects with Internet News (INN), one of the most popular
news server packages. Note that you don't need a news server if you just want to
read Usenet news. For that, you need a news reader, such as tin (http://
www.tin.org), Knews (http://www.matematik.su.se/~kkj/), or Netscape's news
reader component. You also need access to a news server, such as one maintained by
your ISP.

Remote login servers If you want to run programs remotely, you must run some
variety of remote login server. This is a program that accepts logins from remote
locations. A getty program (discussed in Chapter 12) is a login server for dial-up
connections. The most familiar login server for most people is Telnet, which accepts
logins from the Internet at large. This server comes with all major Linux distribu-
b.) Unfortunately, Telnet sends all information, including passwords, in clear-
text, so it's not good from a security point of view. A better alternative in this respect
is the Secure Shell (SSH), which encrypts all data. One implementation of SSH is
OpenSSH (http://www.openssh.com), which became a standard part of Red Hat
Linux with version 7.0 of the description.

Web servers One of the most visible types of Internet server is the Web server,
which implements the Hypertext Transfer Protocol (HTTP). On Linux, Apache
(http://www.apache.org) is by far the most popular Web server. Apache is com-
plex to do more than basic configuration, you should read a book on the
topic, such as Charles Aulds' Linux Apache Server Administration (Syex, 2001).

X servers An X is a program that displays the windows created by X-based
programs. On an isolated workstation installation of Linux, the X server (typically
XFree86) runs on the same computer as the X programs are being run. You can,
however, connect to a remote computer (using a login protocol like Telnet or SSH)
and run programs from that remote system using your local X server. Note that,
unlike most servers, the X server runs on the computer that's most you; the remote
system runs the client programs. This makes sense when you think of it from the pro-
gram's point of view; to the program, the server—and you—are at the distant loca-
tion, and the server provides remote services (a display and input devices). Chapter