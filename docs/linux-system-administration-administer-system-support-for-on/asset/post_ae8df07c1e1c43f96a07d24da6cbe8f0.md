
## Credits

- ACQUISITIONS EDITOR
  Laura Lewin
- DEVELOPMENT EDITOR
  Laura E. Brown
- TECHNICAL EDITOR
  Christopher A. Jones
- COPY EDITOR
  Barry Childs-Helton
- PROJECT COORDINATOR
  Susan Parini
- COVER COORDINATOR
  Constance Petros
- BOOK DESIGNER
  Jim Donohue
- GRAPHICS AND PRODUCTION SPECIALISTS
  Linda Marousek
  Hector Mendoza
  Dina F. Quan
  Mark Yim
- QUALITY CONTROL SPECIALISTS
  Mick Arellano
  Mark Schumann
- PROOFREADER
  Arielle Carole Mennelle
- INDEXER
  C² Editorial Services

## About the Author

Anne H. Carasik, currently an Information Security Analyst for VeriSign, Inc., has worked in the computer industry since 1992 with companies that include IBM, Northern Telecom (Nortel), and Hewlett-Packard. Anne has been active in UNIX- and Internet-related projects since 1994, including the development and teaching of courses; she has also worked as a network systems engineer in Network Security Services at International Network Services.

*To Dad, who introduced me to the world of computers even before my first pacifier.*

## Preface

Welcome to the world of Linux system administration. You're in for some fun and challenges, especially if you like to tinker. System administration is the art of making things run smoothly and handling unexpected events that come your way.

*LINUX System Administration* is a part of the M&T Books Slackware series; it takes off where *LINUX Configuration and Installation, Fourth Edition* leaves off (and you'll see references to that book when installation issues come up).

This book focuses on maintaining Slackware 3.5 – a special bundling of the Linux operating system that includes select utilities from Slackware creator Patrick Volkerding.

### How This Book Is Different

*LINUX System Administration* is a distinctive approach to system administration, detailing support for one user (yourself) as well as for multiple users. Additionally, this book treats security consistently as an area that requires forethought; in too many systems this vital concern is an afterthought, addressed only after the system is in production or connected to the Internet. This book, unlike other system-administration books, shows you how to keep security in the foreground while you're administering the system.

Because a system administrator must understand how Linux interacts with both the user and the computer hardware, you'll also find practical details of the Linux kernel and its functionality, as well as the startup and shutdown scripts.

### Who Should Read This Book

*LINUX System Administration* is not necessarily just for beginners; advanced users will benefit from it too. To get the most from this book, you should be ready to enhance these qualities in your role as system administrator:

- Knowledge of basic UNIX commands from a user's perspective
- An understanding of basic PC hardware
- A willingness to put system security foremost

### What’s in This Book

This book is written so you can either read it in chronological order, or you can use it as a reference. If you are interested in the basics of Linux system administration, look at Chapters 1 through 4; these chapters cover basic installation, system administration responsibilities, as well as hardware and the file system. Chapters 5 through 7 introduce some practical details of actual Linux system administration, including what tools to use, the role of kernel tweaking, and how to use run levels. Chapters 8 through 10 are security-specific, describing account management, host security, and disaster recovery. Chapters 11 and 12 cover networking basics, as well as how Linux is used on the Internet. The appendices list other sources of information that you can find on the Internet or on the CD-ROM.

**Chapter 1 – Slackware Linux Installation.** If you have not installed Slackware already, this chapter reviews system requirements and the basics of installation. It also explains how to monitor performance and addresses some basic security concepts you should think about from the moment you begin to install Slackware Linux.

**Chapter 2 – A System Administrator’s Responsibilities.** This chapter explains the kind of planning a system administrator should be doing—defining goals, establishing security, maintaining accessibility, and handling growth.

**Chapter 3 – File System and Disk Management.** This chapter covers the Linux file structure, including inodes, the second extended file system, and links. It explains how to manage disk usage and swap space.

**Chapter 4 – Devices and Peripherals.** This chapter goes over Linux devices, including SCSI and IDE drives. It also covers the process of mounting devices and examines issues common to peripherals such as printers and mice.

**Chapter 5 – System Administration Tools.** This chapter examines various tools an administrator needs, including tool locations, special permissions of SUID and SGID, using basic UNIX commands as administration tools, proper use of data storage and compression tools, the properties of UNIX processes, methods for scheduling jobs, the basic setup procedure for X, and where to find additional tools.

**Chapter 6 – Kernel Tweaking and Hacking.** This chapter explains the process of kernel rebuilding and how the kernel works. It explains the configuration screens to help you decide what drivers to add and where to add them.

**Chapter 7 – Booting Up and Shutting Down.** This chapter covers LILO, run levels, and system shutdown. Examples of startup and shutdown scripts show how and where these can be used.

**Chapter 8 – Managing User Accounts.** Too many people forget that the cornerstone of good security is maintaining user accounts. This chapter reviews passwords (and how to secure them), permissions, and setting up a Linux environment for your users.

**Chapter 9 – Host Security.** This chapter describes such aspects of security as the types of attack you may face, how to secure your system, and how security tools can help you detect problems on your host.

**Chapter 10 – Disaster Recovery and Backups.** Are you prepared for anything that may corrupt your system or bring it down? This chapter describes different types of local disasters, how to handle them, and offers a backup-strategy approach.

**Chapter 11 – Networking Linux.** This chapter covers some basics of networking – including the TCP/IP protocol suite, the importance of network configuration files, how Linux functions on a network, and useful approaches to dialup connections or direct connectivity.

**Chapter 12 – Linux Internet Applications.** This chapter shows you some e-mail and World Wide Web implementations on Linux. It also addresses two common dangers of the Internet: hackers and spammers.

**Appendix A – Linux Web Sites.** This list of Net destinations can help you make contact with other enthusiastic Linux users, and you can see a sample of the massive information available.

**Appendix B – Linux USENET Newsgroups.** USENET groups are a great place to post questions. This Appendix lists everything from Linux installation help to Linux User Groups all over the world.

**Appendix C – GNU General Public License.** Review this document for information regarding Linux licensing.

**Appendix D – About the CD-ROM.** This appendix lists and describes the contents of the book’s accompanying CD-ROM.

### Icons Used

In the margins, you'll find icons that call your attention to additional insights or commentary.

![](img/8ad518fddafc7f5e73715a2604b61d50_12_0.png)

Security icons provide information for securing your system, a large focus of this book.

![](img/8ad518fddafc7f5e73715a2604b61d50_12_1.png)

Note icons provide additional information about the topic at hand.

![](img/8ad518fddafc7f5e73715a2604b61d50_12_2.png)

Caution icons tell you when to be wary of something occurring when you least expect it. These items may be system-specific behaviors or warnings when typing in delicate commands.
