
![](img/8ad518fddafc7f5e73715a2604b61d50_398_0.png)

The Nomad Mobile Research Center releases a set of Netware cracking tools called Pandora. Be aware that your Linux host on a Novell network is open to the Pandora attacks. Pandora is available at `http://www.nmrc.org`.

## AppleTalk

AppleTalk is Apple's LAN protocol. This protocol uses much simpler addresses than IPX, and is used for file sharing and printing on a Macintosh network. However, AppleTalk does broadcast its services in a fashion similar to that of IPX -- it advertises its services via broadcasts. AppleTalk networks are divided into zones, which section off networks.

The NetaTalk application will let your Linux host look like a shared file server to an AppleTalk server. Compile AppleTalk into your kernel in the Networking Options, and install the `netatalk` package.

![](img/8ad518fddafc7f5e73715a2604b61d50_398_1.png)

To learn more about AppleTalk and Linux, see the NETATALK-HOWTO on the CD-ROM.

## NetBIOS

NetBIOS, or Session Message Block (SMB), is a Microsoft peer-to-peer networking protocol. Enabling SMB on a Linux host lets you share resources such as printers and drives. This works from Windows to Linux or vice versa.

The Linux implementation of SMB is called Samba. The latest version is available at `ftp://nimbus.anu.edu.au/pub/tridge/samba/`; however, you already have a samba package available on the Slackware CD-ROM. Samba is a complex package; read the documentation before you implement it.

There are two daemons that Samba needs to run: `smbd` for the network protocol and `nmbd` for the SMB naming. There are some executables to run SMB commands on your Linux host. There are `smbprint` for printing through an SMB connection, `smbrun` for running applications over an SMB connection, and `smbstatus` to see the status of an SMB connection.

![](img/8ad518fddafc7f5e73715a2604b61d50_399_0.png)

**ON THE CD** For more information on Samba, please see the SMB-HOWTO on the CD-ROM.

## Summary

Networking with Linux is explored in this chapter, along with a variety of networking issues and information; more will emerge. As more people rely on network resources, whether internal, external, or Internet, networking becomes increasingly important.

Computers on networks use networking protocols to talk to each other. Linux, as well as other UNIX operating systems, use *TCP/IP* as their main networking protocol. Other networking protocols that you can run on Linux currently include IPX, Netbios, and Appletalk. Networking protocols can be illustrated with the OSI model. However, *TCP/IP* is best explained with the TCP model: Application, Transport, Network, and Physical layers.

*TCP/IP* classifies network addresses according to three defined network classes (A, B, and C), that correspond to distinctive arrangements of the basic address form aaa.bbb.ccc.ddd. Because typing numerical network addresses can be cumbersome, a naming scheme called Domain Name Service (DNS) applies to IP addresses.

To configure your computer as a host on a network, run */sbin/netconfig*. This sets up the basic IP address, domain name, hostname, gateway address, nameserver, and subnet mask. When you have this configured, it should be easy to connect to a network.

Linux networking uses daemons to control its network servers. These servers include *e-mail* (smpd), *telnet* (telnetd), and *ftp* (ftpd). If someone tries to connect to your host, these servers must be running.

You also have some standard networking configuration files. They define the networks, the hosts, the services, and the protocols that run on your Linux host. Also, you have some files that are designed to protect your host; and others that are designed to be open and trusting.

Linux does not only have to be a host on a network; it can also route network traffic as a router or a firewall. This way you can filter or direct traffic on your network.

For network connectivity, you can connect via a LAN card (NIC card) or a modem. For modem connectivity, you can use a terminal emulator or you can connect via *PPP* or *SLIP*. *SLIP* and *PPP* give you full networking capability on your entire system, where you only have the networking local to the emulator.

## Chapter 12 Internet Applications

**IN THIS CHAPTER**

- Communicating with e-mail
- Using client applications
- Setting up the Apache Web Server
- Examining USENET
- Evaluating Internet dangers

BECAUSE NETWORKING OFTEN connects machines that use a wide range of applications, it's useful for a system administrator to think about how Linux interacts with the applications that are common on private networks and the Internet. These are all TCP/IP-based applications— some are daemons, others are user applications. You may already be familiar with applications such as pine (a popular mail program on UNIX); if so, a review can't hurt.

## Communicating with E-mail

The main reason people get on networks is for communication – in particular, electronic mail (e-mail). Sending electronic messages – for whatever purpose – from one person to another is a universally handy capability. You'll find it implemented platforms as diverse as Windows, legacy mainframes, and UNIX – complete with the advantages and headaches that inevitably go along with e-mail. But near-universal use doesn't necessarily mean a capability is “uniform” across platforms. Slackware Linux e-mail applications work a little differently from those on non-UNIX based platforms.

![](img/8ad518fddafc7f5e73715a2604b61d50_400_0.png)

> For an example of how e-mail can become a headache for many network users, including the administrator, see the section on spam later in this chapter.

## Application Types

E-mail applications are, by and large, pretty straightforward. They work with folders, are menu-driven, are easily customizable, and you have a healthy range of applications to choose from.

Internet e-mail gives you capabilities such as access to USENET newsgroups, downloading files via FTPMAIL, and subscribing to mailing lists. The only thing you can’t do is open a connection to a host so you can telnet or run a shell on it.

Of course, as a Linux user you can always use the obvious-but-cryptic mail command, but you’re generally better off using applications such as pine, elm, or xmh.

### PINE

Pine is a text-based menu driven mailer. It usually reads the mail directly from the spool, or it can use POP or IMAP. As you can see in Figure 12-1, you have several options with pine; for example, you can view folders, your inbox, or your address book from the main menu. Pine has some nice features for working with MIME attachments as well.

![](img/8ad518fddafc7f5e73715a2604b61d50_401_0.png)

Figure 12-1: Pine’s main menu

### ELM

Elm is also a text-based menu driven mailer. Elm works a little differently than pine, where it opens up your inbox automatically and your options are following, as shown in Figure 12-2. You can open up other mailboxes or go to your aliases. I find elm is easier to configure, but many people like to use pine. As is common with many personal choices – including such technical preferences as operating systems – you may find a “religious war” raging over this topic. (It may or may not be safer to talk about than politics.)

![](img/8ad518fddafc7f5e73715a2604b61d50_402_0.png)

Figure 12-2: Elm's main menu

### XMH

The *xmh* mailer is a graphical interface to receiving mail. Instead of using a text-based menu, you use the menu options from the top, as shown in Figure 12-3. Don't let appearances fool you; xmh is a sophisticated mailer.

![](img/8ad518fddafc7f5e73715a2604b61d50_403_0.png)

Figure 12-3: xmh's main menu

### Mailing Lists

E-mail has proven its worth as a highly effective means of group communication. People can read these messages at their convenience, and normally the number of people on a list need not be limited. Of course, spam happens; many public lists have more noise than their users would like. Some mailing lists generate hundreds of e-mail messages a day. For those who are interested in discussing a particular topic, it’s a boon. For others, it may look like spam.

Two popular types of automated mailing-list software are Majordomo and Listserv.

#### MAJORDOMO

Majordomo is a popular freeware program that automates Internet mailing lists. Majordomo commands are sent via electronic mail to handle all aspects of list maintenance. When a list is set up on the server, most Majordomo functions can be performed remotely.

Majordomo does not handle the mail directly, as do sendmail and qmail, but it does control the lists’ e-mail addresses and content. However, it does have the ability to archive the messages if desired.

Majordomo supports moderated lists, archives, remote message retrieval, digests, and support for FTPMAIL. It also supports confirming subscribing and unsubscribing, and provides some protection against forged subscriptions. Listing 12-1 shows the help file for Majordomo.
