# 530 Chapter 15 TCP/IP Linux Networking

Several GUI front-ends to smbount available. Details of operation differ from one program to another, but as a general rule, these utilities present a GUI of the local network, as demonstrated by LinNeighborhood (http://www.bnro.de/~schmidjo/), shown in Figure 15.4. When you double-click a share to open it, a dialog box asks for your username and password, and the program opens a window on the share using the file manager you specify when you configure the program. GUI front-ends don't really add fundamentally new functionality to Linux's SMB/CIF capabilities, but they do make these networks more accessible to those who aren't familiar with Samba's text-mode tools. You may therefore want to install LinNeighborhood, or a similar package, such as Kruiser (http://devel-home.kde/~kruiser/) or xSMBrowser (http://www.public.iasstate.edu/~chadpen/).

# Internet Servers

If you want to use a computer when you're away from it, you must install some variety of server on that computer. Likewise, if you want others to be able to use a computer, a server is necessary. The appropriate server depends on your precise needs, there are some commonalities to configuring servers, but every one involves at least some aspects, so you should consult the appropriate documentation.

# Available Servers

Linux supports a wide variety of Internet server packages. Although these can be used on a local network alone, they're more often used to provide services to a wide variety of computers on the Internet at large. A few of these servers are discussed to a greater or lesser extent elsewhere in this book. Many are complex enough that entire books are written about them. You can usually find more information in documentation files that contain the servers, or on Web pages devoted to the servers. A complete listing of servers available for Linux would be too long to reproduce; some of the most important server types include:

+   * FTP servers The File Transfer Protocol (FTP) is one of the most important protocols, although it's one of the least flashy. FTP allows individuals to transfer files to from an FTP server. Links on Web pages to program files are often FTP links. Several FTP servers are available for Linux, such as Washington University FTP (WU-FTP; http://wu-ftp.org/) and ProFTP (http://proftp.net). Red Hat Linux ships with WU-FTP, but you can install any other FTP server for Linux, if you prefer.

+   * Mail servers If you want your computer to receive mail addressed directly to it, you must run a mail server—a.k.a. a Mail Transport Agent (MTA). If your ISP collects