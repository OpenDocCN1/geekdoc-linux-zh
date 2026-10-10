
## Web Servers

Most Linux distribution includes Apache (`http://www.apache.org`). Apache is the number one server on the Internet (`http://www.netcraft.co.uk/survey/`); more than a half of all Internet sites are running Apache or one of its derivatives. Apache advantages include its modular design, stability, and speed. Given the appropriate hardware and configuration, it can support the highest loads. Yahoo, AltaVista, GeoCities, and Hotmail are based on customized versions of this server.

Optional support for SSL (which enables secure transactions) is also available at:
- `http://www.apache-ssl.org/`
- `http://raven.covalent.net/`
- `http://www.c2.net/`

Related HOWTOs can be found at:
- `http://MetaLab.unc.edu/mdw/HOWTO/WWW-HOWTO.html`
- `http://MetaLab.unc.edu/mdw/HOWTO/Virtual-Services-HOWTO.html`
- `http://MetaLab.unc.edu/mdw/HOWTO/Intranet-Server-HOWTO.html`

Web servers for Linux can be found at `http://www.linuxlinks.com/Software/Internet/WebServers/`.

## Web Browsers

A number of Web browsers exist for the Linux platform. Netscape Navigator is one of the choices, available from the very beginning, and the upcoming Mozilla (`http://www.mozilla.org`) will have a Linux version. Another popular text-based Web browser is Lynx. It is fast and handy when no graphical environment is available.

Browser software for Linux can be found at `http://www.linuxlinks.com/Software/Internet/WebBrowsers/`, and at `http://MetaLab.unc.edu/mdw/HOWTO/mini/Public-Web-Browser.html`.

## FTP Servers and Clients

FTP stands for File Transfer Protocol. An FTP server allows clients to connect to it and retrieve (download) files. Many FTP servers and clients exist for Linux and are usually included with most distributions. There are text-based clients as well as GUI-based ones. FTP-related software (servers and clients) for Linux may be found at `http://MetaLab.unc.edu/pub/Linux/system/network/file-transfer/`.

## News Service

Usenet (also known as news) is a big bulletin board system that covers all kind of topics and is organized hierarchically. A network of computers across the Internet (Usenet) exchange articles through the NNTP protocol. Several implementations exist for Linux; either for heavily loaded sites or small sites receiving only a few newsgroups.

The INN home page can be found at `http://www.isc.org/`. Linux news-related software can be found at `http://www.linuxlinks.com/Software/Internet/News/`.

## Domain Name System

A DNS server has the job of translating names (readable by humans) to an IP address. A DNS server does not know all the IP addresses in the world; rather, it is able to request other servers for the unknown addresses. The DNS server will either return the wanted IP address to the user or report that the name cannot be found in the tables.

Name serving on Unix (and on the vast majority of the Internet) is done by a program called named. This is a part of the bind package of The Internet Software Consortium.

The BIND home page can be found at `http://www.isc.org/`. The DNS HOWTO can be found at `http://www.MetaLab.unc.edu/LDP/HOWTO/DNS-HOWTO.html`.

## DHCP, Bootp

DHCP and bootp are protocols that allow a client machine to obtain network information (such as their IP number) from a server. Many organizations are starting to use it because it eases network administration, especially in large networks or networks that have lots of mobile users.

## NIS

The Network Information Service (NIS) provides a simple network lookup service consisting of databases and processes. Its purpose is to provide information, which has to be known throughout the network, on all machines on the network. It allows, for example, for one person to log on to any machine in the network running NIS without the need for the administrator to add a password entry for him in all the machines, only in the main database.

The NIS HOWTO can be found at `http://Metalab.unc.edu/~mdw/HOWTO/NIS-HOWTO.html`.

## Authentication

There are also various ways of authenticating users in mixed networks. For Linux/Windows NT, go to `http://www.mindware.com.au/ftp/smb-NT-verify.1.1.tar.gz`. For the PAM (pluggable authentication module), which is a flexible method of Unix authentication, go to the PAM library at `http://www.kernel.org/pub/linux/libs/pam/index.html`. For LDAP in Linux, go to `http://www.umich.edu/~dirs CVS/ldap/index.html`.

## REMOTE EXECUTION OF APPLICATIONS

One of the most amazing features of Unix (yet one of the most unknown to new users) is the great support it provides for the remote and distributed execution of applications.

### Telnet

Telnet is a program that allows a person to use a remote computer as if that person was actually at that site. Telnet is one of the most powerful tools for Unix, allowing for true remote administration. It is also an interesting program from a user’s point of view, because it allows remote access to all their files and programs from anywhere in the Internet. Combined with an X server, there is no difference (apart from the delay) between being at the console or on the other side of the planet. Telnet daemons and clients are available with most Linux distributions.

Encrypted remote shell sessions are available through SSH (`http://www.cs.hut.fi/ssh/`), thus effectively allowing secure remote administration. For Telnet-related software, go to `http://MetaLab.unc.edu/pub/Linux/system/network/telnet/`.

### Remote Commands

In Unix, and Linux in particular, remote commands exist that allow for interaction with other computers from the shell prompt. Two examples are rlogin, which allows for login from a remote machine in a similar way to telnet and rcp, which allows for remote transfer of files among machines. Finally, the remote shell command rsh allows the execution of a command on a remote machine without actually logging onto that machine.

### X Window

The X Window system was developed at MIT in the late 1980s and is rapidly becoming the industry standard windowing system for Unix graphics workstations. The software is freely available, very versatile, and suitable for a wide range of hardware platforms. Any X Window system consists of 2 distinct parts: the X server and 1 or more X clients. It is important to realize the distinction between the server and the clients. The server controls the display directly and is responsible for all input/output via the keyboard, mouse, or display. The clients, on the other hand, do not access the screen directly—they communicate with the server, which handles all input and output. It is the clients that do the “real” computing work—running applications or whatever. The clients communicate with the server, causing the server to open one or more windows to handle input and output for that client.

In short, the X Window system allows a user to log in to a remote machine, execute a process (for example open a Web browser), and have the output displayed on his own machine. Because the process is actually being executed on the server, very little CPU power is needed by the client. Indeed it is possible to have computers whose primary purpose is to act as pure X Windows servers and they are known as X terminals.

A free port of the X Window system exists for Linux and can be found at Xfree at `http://www.xfree86.org/`. It is usually included in most Linux distributions.

The related remote X Apps HOWTO can be found at `http://MetaLab.unc.edu/mdw/HOWTO/mini/Remote-X-Apps.html`.

## Networking Overview

163

## VNC

VNC stands for Virtual Network Computing. It is, in essence, a remote display system that allows you to view a computing “desktop” environment not only on the machine where it is running but also from anywhere on the Internet and from a wide variety of machine architectures. Both client and server exist for Linux as well as for many other platforms. It is possible to execute MS Word on a Windows NT or 95 machine and have the output displayed on a Linux machine. The opposite is also true. It is possible to execute an application on a Linux machine and have the output displayed on any other Linux or Windows machine. A Java client exists, which allows you to run the remote display inside a Web browser. Finally a port for Linux using the SVGAlib graphics library allows 386s with as little as 4 Mb of RAM to become fully functional X Terminals. The VNC Web site can be found at `http://www.orl.co.uk/vnc/`.

## NETWORK INTERCONNECTION

Linux networking is rich in features. A Linux box can be configured to act as a router, a bridge, etc. Some of the available options are described below.

### Router

The Linux kernel has built-in support for routing functions. A Linux box can act either as an IP or an IPX router for a fraction of the cost of a commercial router. Recent kernels include special options for machines acting primarily as routers:
- **Multicasting**: Allows the Linux machine to act as a router for IP packets that have several destination addresses. It is needed on the MBONE, a high bandwidth network on top of the Internet which carries audio and video broadcasts.
- **IP policy routing**: Normally, a router decides what to do with a received packet based solely on the packet’s final destination address, but routing can also take into account the originating address and the network device from which the packet reached it.

There are some related projects, including one aimed at building a complete running Linux router on a floppy disk, which can be found at `http://www.psychohis.com/linux-router/`.

Part III
