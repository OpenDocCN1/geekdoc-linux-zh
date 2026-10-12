
## LISTING 18.15 continued

```
.ascii  "TEXT"  "ttxt"  ASCII Text  SimpleText
→text/plain
.text  "TEXT"  "ttxt"  ASCII Text  SimpleText
→text/plain
.txt  "TEXT"  "ttxt"  ASCII Text  SimpleText
→text/plain
.faq  "TEXT"  "ttxt"  ASCII Text  SimpleText
→text/x-usenet-faq
.a  "TEXT"  "ttxt"  Assembly Source  SimpleText
.asm  "TEXT"  "ttxt"  Assembly Source  SimpleText
.bas  "TEXT"  "ttxt"  BASIC Source  SimpleText
.boo  "TEXT"  "ttxt"  BOO encoded  SimpleText
.bib  "TEXT"  "ttxt"  BibTeX Bibliography  SimpleText
.bst  "TEXT"  "ttxt"  BibTeX Style  SimpleText
.info  "TEXT"  "ttxt"  Info Text  SimpleText
application/text
.bat  "TEXT"  "ttxt"  MS-DOS Batch File  SimpleText
.cmd  "TEXT"  "ttxt"  OS/2 Batch File  SimpleText
.me  "TEXT"  "ttxt"  Text Readme  SimpleText
.rme  "TEXT"  "ttxt"  Text Readme  SimpleText
.1st  "TEXT"  "ttxt"  Text Readme  SimpleText
application/text
.readme  "TEXT"  "ttxt"  Text Readme  SimpleText
application/text
.ini  "TEXT"  "ttxt"  Windows INI File  SimpleText
.ps  "TEXT"  "vgrd"  PostScript  LaserWriter 8
application/postscript
.eps  "EPSF"  "vgrd"  Postscript  LaserWriter 8
application/postscript
.epsf  "EPSF"  "vgrd"  Postscript  LaserWriter 8
application/postscript
.dvi  "ODVI"  "xdvi"  TeX DVI Document  xdvi
application/x-dvi
```

As you can see, this file is quite comprehensive and you should probably not have to edit it by hand, unless you want to add support for a new file type not already included here.

## AppleVolumes.default

The last file to consider is the AppleVolumes.default, which is shipped with the netatalk package and contains a single uncommented line with a tilde character on it. This tilde character indicates that user home directories should be made available to AppleTalk clients who connect to this server. Although this is quite useful, if it is not enough, you can use the information in the file itself and in the afpd manual page to make other filesystems available to AppleTalk clients.

## Starting the Netatalk Server

Finally we reach the moment of truth, for now it is time to start the netatalk servers and determine if they work. In order to start the servers, you are encouraged to use the atalk script installed in /etc/rc.d/init.d by the netatalk package. This is a standard System V style script and to start the AppleTalk services, you would issue the following command:

```
/etc/rc.d/init.d/atalk start
```

Assuming no error messages, you can verify that the servers are working by going to a Mac client on your network, opening the chooser, and clicking on AppleShare. If you have everything configured correctly, you should be able to see your Linux system. Clicking on your server name should result in a password prompt and you can log in as any non-root user that has a shell and a password of eight or fewer characters.

## Summary

This chapter briefly covered how Linux can be used to offer services to NetWare and AppleTalk clients in a network. You also saw how Linux can be used as a NetWare client. This ability of Linux to interoperate with multiple network operating systems is a big part of the reason why Linux is so popular. And the work to allow Linux to interoperate with other network operating systems is continuing. Examples of this are projects to add protocols such as DecNET to Linux. If your favorite network protocol is not yet supported, stay tuned.

## Internet Services

## PART VI

## In This Part

- 19 Setting Up Internet Services 529
- 20 Electronic Mail 553
- 21 FTP and Anonymous FTP 609
- 22 Web Serving 637
- 23 News Services 671
- 24 Internet Telephony and Conferencing 713
- 25 Security Principles 739

## Setting Up Internet Services

## In This Chapter

- Choosing Services to Offer 530
- The Internet Server inetd 531
- Using TCP-Wrappers 534
- xinetd as an Alternative to inetd 538
- Standard Services: Remote Login, Execution, and File-Copy 541

This chapter discusses how to set up Internet services on a Red Hat Linux system. It concentrates on the most fundamental services: remote login, remote command execution, and remote file copy facilities. It also discusses issues of access control and security relating to the provision of these services.

## Choosing Services to Offer

Deciding which Internet services to offer is an important part of a system administrator's role. If users don't have access to the services they need, they won't be able to do their own jobs; yet providing more services than are necessary adds to the administrator's workload and may compromise system security.

When deciding what services to offer, it is important to draw a distinction between internal and external users, especially when external users are allowed to connect from anywhere on the Internet. In a typical organization, internal users would be those with explicit written permission to use the facilities provided, such as employees, whereas external users would be, essentially, the general public. Not all users are this easy to categorize, though; for example, different organizations might need to classify telecommuters in different ways.

It is undeniable that some external would-be users have malicious intent. It can be very hard to verify the identity of external users before granting access to a service, and it can be even harder to track down anyone who attacks the system. Internal users have a much greater degree of accountability—quite possibly including contractual terms under which unauthorized use constitutes grounds for dismissal—and therefore can be trusted with a greater degree of responsibility. (Of course, this is not to say that internal users are invariably entirely trustworthy.) In the majority of situations, external users are offered only a limited range of informational services; the services described in this chapter would typically be reserved for users known to have more responsibility.

## Low-Level Services

The services that run on a machine can be broadly divided into a number of groups. The lowest-level services provide fundamentals of the actual networking system. They include the routing protocols and name services described in Chapter 14, “TCP/IP and Ethernet,” and if all is well, these are invisible to users. The next step up is the services that form the infrastructure of a network—the printing and file-sharing services that were dealt with in Chapter 15, “Sharing Resources,” as well as interoperability with other systems and networks (including Windows, NetWare, and AppleTalk), described in Chapters 17, “Integrating with Windows NT Networks,” and 18, “Integrating with Other Network Operating Systems.” The Internet services that are the subject of this chapter form the next higher level.

## Internet Services

Some Internet services will be required on almost every system. One such service is email, which is a requirement at most sites, if only for local delivery of warning messages from Cron jobs and the like. Indeed, in many organizations, email will be one of the fundamental means of internal communication. Internet email using standard protocols such as SMTP, POP, and IMAP is dealt with in Chapter 20, “Electronic Mail.”

## Remote Login Service

Similarly, almost all sites will need some form of remote login or remote execution service. On UNIX systems, the usual choice is between Telnet, Rsh/Rlogin, and SSH; all of these services are described in detail in this chapter. I will also discuss the particularly strong security requirements of remote login and remote execution facilities.

## Other Internet Services

Most of the other common Internet services can be broadly classified as information-providing. FTP, Usenet News, and World Wide Web services are among the most common, and each is covered in its own chapter in this book: see Chapter 21, “FTP and Anonymous FTP,” Chapter 22, “Web Serving,” and Chapter 23, “News Services.” Web servers in particular are becoming ever more important for distributing static and dynamic information to both internal and external users. FTP archives and Usenet News will not be as widely needed, especially as services that must be made available to external users.

Once you have decided which services to offer, the next step is to make those services available. This is the subject of the remainder of this chapter.

## The Internet Server inetd

The daemons providing many network services can be run by the so-called Internet super-server, inetd (pronounced “eye-net dee”). This daemon listens for connections on certain network ports; precisely which ports depends on how it is configured locally. When it receives connections, it invokes a program which will service that connection, again using local configuration to decide which program to run. Essentially, inetd multiplexes a number of daemons into a single one to ease configuration and reduce system load. It also makes it easier for programmers to write network daemons because it does the work of listening for and accepting connections.
