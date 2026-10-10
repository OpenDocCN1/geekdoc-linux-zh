
## 10.3.3.3 Proxy servers

### 10.3.3.3.1 What is a proxy server?

Companies and organizations often want their users to use a proxy server. Especially in environments with lots of users, a proxy server can enable faster downloads of web pages. The proxy server stores web pages. When a user asks for a web page that has already been requested previously, the proxy server will give that page to the user directly, so that s/he does not need to get it from the Internet, which would take longer. Of course, measures can be taken so that the proxy server does a quick check and always serves the most recent version of a page. In some environments, usage of the proxy server is compulsory, in other environments you may have the choice whether or not to use it.

### 10.3.3.3.2 Proxy configuration

If you have the proxy server name and port, it should be rather obvious to feed that information into your browser. However, many (command line) applications depend on the variables **http_proxy** and **ftp_proxy** for correct functioning. For your convenience, you might want to add a line like the following to your ~/.bashrc:

```
export http_proxy=http://username:password@proxy_server_name:port_number
```

For instance:

```
export http_proxy=http://willy:Appelsj3ntj3@proxy:80
```

If you do not need to give a username and password, simply leave out everything before the "@" sign, this sign included.

## 10.3.4 File Transfer Protocol

### 10.3.4.1 FTP servers

On a Linux system, an FTP server is typically run from **xinetd**, using the WU-ftpd server, although the FTP server may be configured as a stand-alone server on systems with heavy FTP traffic. See the exercises.

Other FTP servers include among others vsftpd, Ncftpd and Proftpd.

Most Linux distributions contain the anonftp package, which sets up an anonymous FTP server tree and accompanying configuration files.

### 10.3.4.2 FTP clients

Most Linux distributions include **ncftp**, an improved version of the common UNIX **ftp** command, which you may also know from the Windows command line. The **ncftp** program offers extra features such as a nicer and more comprehensible user interface, file name completion, append and resume functions, bookmarking, session management and more:

```
thomas:> ncftp blob
NcFTP 3.0.3 (April 15, 2001) by Mike Gleason (ncftp@ncftp.com).
Connecting to blob...
blob.some.net FTP server (Version wu-2.6.1-20) ready.
Logging in...
Guest login ok, access restrictions apply.
Logged in to blob.
ncftp /> help
Commands may be abbreviated. 'help showall' shows hidden and
unsupported commands.
'help <command>' gives a brief description of <command>.

ascii    cat      help     lpage    open     quote    site
bgget    cd       jobs     lpwd     page     rename   type
bgput    chmod    lchmod   lrename pdir     help     umask
close    ll       lln      lrm    pie      rm       version
debg     lll      lmkdir   put    rmdir
bookmark get      lookup   mkdir  pwd      set
ncftp / >
```

Excellent help with lot of examples can be found in the man pages. And again, a number of GUI applications are available.

> **FTP is insecure!**
> 
> Don't use the File Transfer Protocol for non-anonymous login unless you know what you are doing. Your user name and password might be captured by malevolent fellow network users! Use secure FTP instead; the **sftp** program comes with the Secure Shell suite, see Section 10.4.4.4.

## 10.3.5 Chatting and conferencing

Various clients and systems are available in each distribution, replacing the old-style IRC text-based chat. A short and incomplete list of the most popular programs:

- **gaim**: multi-protocol instant messaging client for Linux, Windows and Mac, compatible with MSN Messenger, ICQ, IRC and more; see the Info pages or the Gaim site <http://gaim.sourceforge.net/> for more.
- **xchat**: IRC client for the X window system:

The home page is at SourceForge <http://sourceforge.net/projects/xchat/>.

- aMSN: an MSN clone.
- Konversation, kopete, KVIrc and many other K-tools from the KDE suite.
- gnomeeeting: videoconferencing program for UNIX (now Ekiga).
- jabber: Open Source Instant Messaging platform, compatible with ICQ, AIM, Yahoo, MSN, IRC, SMTP and much more.
- psi: jabber client, see the PSI Jabber Client Homepage <http://psi.affinx.com/>.
- skype: program for making telephone-like calls over the Internet to other Skype users, see <http://www.skype.com> for more info. Skype is free but not open.
- Gizmo: a free (but not open) phone for your computer, see <http://www.gizmoproject.com>.

## 10.3.6 News services

Running a Usenet server involves a lot of expertise and fine-tuning, so refer to the INN homepage <http://www.isc.org/> for more information.

There are a couple of interesting newsgroups in the comp.* hierarchy, which can be accessed using a variety of text and graphical clients. A lot of mail clients support newsgroup browsing as well, check your program or see your local Open Source software mirror for text clients such as tin, slrn and mutt, or download Mozilla or one of a number of other graphical clients.

Deja.com <http://deja.com/> keeps a searchable archive of all newsgroups, powered by Google. This is a very powerful instrument for getting help: chances are very high that somebody has encountered your problem, found a solution and posted it in one of the newsgroups.

## 10.3.7 The Domain Name System

All these applications need DNS services to match IP addresses to host names and vice versa. A DNS server does not know all the IP addresses in the world, but networks with other DNS servers which it can query to find an unknown address. Most UNIX systems can run named, which is part of the BIND (Berkeley Internet Name Domain) package distributed by the Internet Software Consortium. It can run as a stand-alone caching nameserver, which is often done on Linux systems in order to speed up network access.

Your main client configuration file is `/etc/resolv.conf`, which determines the order in which Domain Name Servers are contacted:

```
search somewhere.org
nameserver 192.168.42.1
nameserver 193.74.208.137
```

More information can be found in the Info pages on named, in the `/usr/share/doc/bind[-version]` files and on the Bind project <http://www.isc.org/products/BIND> homepage. The DNS HOWTO <http://www.tldp.org/HOWTO/DNS-HOWTO.html> covers the use of BIND as a DNS server.

## 10.3.8 DHCP

DHCP is the Dynamic Host Configuration Protocol, which is gradually replacing good old **bootp** in larger environments. It is used to control vital networking parameters such as IP addresses and name servers of hosts. DHCP is backward compatible with **bootp**. For configuring the server, you will need to read the HOWTO.

DHCP client machines will usually be configured using a GUI that configures the `dhcpd`, the DHCP client daemon. Check your system documentation if you need to configure your machine as a DHCP client.

## 10.3.9 Authentication services

### 10.3.9.1 Traditional

Traditionally, users are authenticated locally, using the information stored in `/etc/passwd` and `/etc/shadow` on each system. But even when using a network service for authenticating, the local files will always be present to configure system accounts for administrative use, such as the root account, the daemon accounts and often accounts for additional programs and purposes.

These files are often the first candidates for being examined by hackers, so make sure the permissions and ownerships are strictly set as should be:

```
bob:~> ls -l /etc/passwd /etc/shadow
-rw-r--r--   1 root     root        1803 Mar 10 13:08 /etc/passwd
-r--------   1 root     root        1116 Mar 10 13:08 /etc/shadow
```

### 10.3.9.2 PAM

Linux can use PAM, the Pluggable Authentication Module, a flexible method of UNIX authentication. Advantages of PAM:
