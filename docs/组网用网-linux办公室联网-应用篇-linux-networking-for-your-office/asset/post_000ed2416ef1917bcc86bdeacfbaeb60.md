
## Configuring Linux Networking

## PART II

## IN THIS PART

- 5 : Basic Linux Configuration 107
- 6 : Compiling a Kernel for Networking 139
- 7 : Setting Ethernet Options 161
- 8 : Using PPP for Dialup Connections 185

## Basic Linux Configuration

## CHAPTER
5

## IN THIS CHAPTER

- - Installing Linux 108
- - Configuration Files and Tools 124
- - Setting Up User Accounts 131
- - Summary 137

So far you’ve learned background information that’s vital to setting up networking in Linux. This chapter begins a discussion of more practical issues, including how to install Red Hat Linux 6.0. If you’re familiar with Linux installation and the reasons for configuration choices, you can skip much of this chapter. If you’re relatively new to Linux or other UNIX-like operating systems, you should read this chapter carefully because it is vital to understanding how Linux operates.

This book comes with a copy of Red Hat Linux 6.0, one of the most popular distributions of Linux. The section on installing Linux contains some very specific information on this particular distribution and version, but many of the general concerns and principles described apply to other distributions, as well. Throughout the rest of the book, I refer to the linuxconf configuration tool Red Hat provides and that is also used by the Mandrake distribution, which is closely related to Red Hat.

Throughout this book I provide information on how to configure a system using textual configuration tools (that is, manually), so you should be able to configure any Linux system using the information in this book. Linux distributions sometimes vary in where configuration files are located and what they’re called, but for the most part my descriptions of how to configure a system manually should be helpful whether you’re using Red Hat or some other distribution. Some distributions, such as SuSE and Caldera, come with graphical user interface (GUI) configuration tools that are similar to linuxconf in principle, but not in detail. If you’re using such a distribution, you might want to investigate these tools.

### Installing Linux

If all goes well, installing Linux can take as little as about half an hour. Most people who are not familiar with Linux will take longer to install it, however, and situations such as configuring a computer to dual-boot between Linux and another operating system (OS) can increase the required installation time. If you’re diligent about preparing for installation, you might invest an extra half-hour or so at the start. If you’re not, you’ll save that time, but there’s a good chance you’ll spend at least as much going back to check on hardware details or repeating an installation.

Red Hat normally releases a new version of Linux every 3–6 months, so there’s a good chance that by the time you read this the 6.0 distribution included with this book will be a version or two behind the times. If you want to be absolutely current, you can obtain a new version in several ways:

- - Buy an official Red Hat CD from your favorite computer retailer. The list price for Red Hat 6.0 is $79.95, and future versions are likely to be about the same. An official Red Hat package includes technical support, a printed manual, and both demos and fully functional commercial packages not included in the unofficial CDs.
- - Buy an unofficial Red Hat CD from a company such as Cheap*Bytes (http://www.cheapbytes.com), Linux System-Labs (http://www.lsl.com), or Linux Central (http://www.linuxcentral.com). These CDs typically sell for about $2 plus shipping (which is generally about $5 in the United States).
- - Download Red Hat from the Net. You'll need either a fast Internet connection or a great deal of patience to do this (a full download by modem is likely to take a day or more). Red Hat maintains a list of mirror sites that provide Red Hat at http://www.redhat.com/mirrors.html. If you want to install Red Hat from a hard disk partition or create your own installation CD-ROM, you should probably check my Web page on the topic at http://members.bellatlantic.net/~smithrod/rhjo1.html. If you have a direct Internet connection, you can install directly from an FTP site, without storing a copy locally.

The advantage to installing the latest and greatest version of Linux is that you'll be completely up-to-date on performance and security improvements, possibly including new drivers for some of your hardware. The disadvantage is that your experiences may not match what's described in this book as precisely as if you used the version on the book's CD-ROM.

The version of Red Hat 6.0 included on the CD-ROM includes all the updated packages Red Hat has posted to its Web site, up to the day the CD-ROM was mastered. Nonetheless, you might want to check the Red Hat errata page at http://www.redhat.com/errata/ after installing and check to see if there are any important-sounding bug fixes listed there.

The CD-ROM that accompanies this book includes some extra programs that don't normally come with Red Hat Linux, such as the Netatalk server. You should be able to use these packages even with an updated version of Red Hat or with another distribution.

### Partitioning Your Hard Drives

If you want to repartition a system that contains Windows or some other OS, you have two choices:

- - Back up all your data, repartition the system, and restore the data. This is effective, but tedious.
- - Use a utility such as the freeware First Nondestructive Interactive Partition Splitting Program (FIPS; included on the CD-ROM that accompanies this book) or the commercial Partition Magic from PowerQuest (http://www.powerquest.com). Partition Magic is a very handy utility you can use to create and modify Linux partitions in addition to DOS, OS/2, and Windows partitions. It comes with both DOS and Windows executables, including a bootable DOS disk image you can copy to floppy from Linux, so it can be used on a Linux-only system. Figure 5.1 shows Partition Magic in operation.
