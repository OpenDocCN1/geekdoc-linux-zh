
- Linux Parallel Port Home Page 749
- NSBD: Not-So-Bad Distribution 749
- Linux PCMCIA Information 749
- BIND, DHCP, INN Home Page (ISC Consortium) 749
- LinModems 750
- Linux IP Masquerade Resource 750
- DNS tools 750
- Netatalk—Essential for Apple Connectivity 750
- Anders: Netatalk: Linux Netatalk-HOWTO 750
- Samba 750
- Linux Plug-Ins for Netscape 750
- XFree86 Servers by SuSE 750
- Third-Party QuickCam Software Page 750
- The Mesa 3D Graphics Library 751
- WhirlGIF 2.01 751
- BTTV Page Frame Grabber for Linux 751
- XVidCap—X Video Capture for Linux 751
- kwintv 751

## Index 753

## About the Authors

David Bandel earned a Master of Aviation Management from Embry-Riddle Aeronautical University in 1989 at Ft. Campbell, Kentucky. He retired from 20 years in the Army in February, 1996. While on active duty, he learned many of the basics of UNIX working on DEC 5000s running Ultrix and Sun SPARCstations running SunOS 4. He has worked on a variety of systems and architectures, including SPARC Solaris, HP-UX, AIX, and SCO OpenServer. In 1993, he began dabbling with Linux, a hobby that quickly grew on him. Currently, David is semi-retired and living in the Republic of Panama where he writes, does Linux/UNIX consulting, and works on his farm. He co-authored *Que’s Special Edition Using OpenLinux*. He can be reached at david@pananix.com.

Robert Napier has been playing in and around Linux since about 1995. His current pet project is keeping up with KDE2 development. Professionally, he has spent most of his time developing software and supporting various UNIX-like systems. Currently he spends most of his time supporting Perl and writing scripts in RTP for Cisco Systems, spending what time he can to write books on the side. Rob also co-authored *Special Edition Using Linux, Fifth Edition*. Robert can be reached at rnapier@employees.org.

## Dedication

*David Bandel:* Dedicated to my wife, Silvia, my children, and the entire Linux community.

*Robert Napier:* To Janet, who kept my life in order during this distraction.

## Acknowledgments

**David Bandel:** Special thanks go to a number of folks who’ve made this book possible. First and foremost, to my wife, who still doesn’t understand deep hack mode, but tolerates it anyway. Without her support, none of this would have been possible. Thanks also to Erik Ratcliffe at Caldera for his help and diligence in technical editing the book. Erik not only contributed his talent for technical review, but also acted as liaison with some of Caldera’s engineers who like to surprise us all with changes. Thanks to the folks on the Caldera mailing list. They remind me daily how bewildering all this can be to Linux newbies. They also remind me just how small the world really is, and how diverse and widespread the Linux community has become.

Thanks to all the software programmers, particularly the kernel hackers who’ve made all this possible, a number of whom have slipped out of deep hack mode long enough to respond to questions about their code, including Richard Gooch (devfs) and Rusty Russell (netfilter). Thanks also to the entire Linux community, especially the recent converts to Linux.

We are grateful also to Macmillan, particularly Gretchen Ganser and Maureen McDaniel and their team, for wanting to publish a reference like this and putting up with this author’s nit.

**Robert Napier:** First and foremost, I would like to thank my wife, Janet. Many months ago, when we were first considering this project, I said that it would probably take over all of my “home” time. She told me to take care of the writing and she would take care of the rest. True to her word, she has, and it’s meant much more to the success of this book than any of my meager writing talents.

Because this is my first time as a lead author, I would like to thank the man who got me started in this business, Steve Burnett. Steve gave me my first break by allowing me to write a couple of chapters for the fifth edition of this book. His continuing advice and assistance since then has been invaluable to my career as an author.

I would also like to thank my co-author, David Bandel. I’m really glad that at least one of us knew what we were doing.

Since my first writing assignment for Macmillan Publishing, I have worked several times with Gretchen Ganser and Maureen McDaniel. During this book in particular, they have been incredibly helpful in keeping me organized, on time, and in the right direction. At the same time, they have shown incredible flexibility and patience with me. Thank you.

Finally, I would like to acknowledge all the incredible open-source developers out there. In particular, I have had the pleasure of following the KDE2 project very closely over many months now. These guys have done a much better job of managing all the conflicting interests of features versus schedules and stability than most of the software companies I’ve worked with. Thanks to groups like these and so many others like it, the world is finally learning what we’ve known all along: open source works.

## Tell Us What You Think!

As the reader of this book, *you* are our most important critic and commentator. We value your opinion and want to know what we’re doing right, what we could do better, what areas you’d like to see us publish in, and any other words of wisdom you’re willing to pass our way.

As an associate publisher for Sams, I welcome your comments. You can fax, email, or write me directly to let me know what you did or didn’t like about this book—as well as what we can do to make our books stronger.

*Please note that I cannot help you with technical problems related to the topic of this book, and that due to the high volume of mail I receive, I might not be able to reply to every message.*

When you write, please be sure to include this book’s title and author as well as your name and phone or fax number. I will carefully review your comments and share them with the author and editors who worked on the book.

Fax: 317-581-4666<br>
Email: quetechnical@macmillanusa.com<br>
Mail: Associate Publisher<br>
Que<br>
201 West 103rd Street<br>
Indianapolis, IN 46290 USA

## Introduction

### In This Introduction

- Linux Today 2
- A Word About Hardware 3
- About This Book 4
- Who Should Use This Book? 4
- Who Should Not Use This Book? 5
- Conventions Used in This Book 5

### Linux Today

For those of you who haven’t been hiding under a rock during the past few years, you almost couldn’t help hearing about Linux. It has been in all the tabloids, magazines, even on TV and radio news. Several Linux companies have gone public with stocks trading on the open market, and some have even bought out other companies. One historic purchase happened when Caldera Systems bought most of the Santa Cruz Operation (SCO) that sold SCO OpenServer and SCO UnixWare.

All this is a long way for a previous guerrilla operating system to come. Introduced little by little through the back door into the Fortune 1000 companies and other places, Linux gained management attention and recognition with uptimes and reliability Microsoft could only dream of. At first these companies hid their use of Linux, often denying they used the “little OS that could.” But servers sitting on the Internet are hard to hide, as are systems administrators proud that they could solve a problem the company had been struggling with for a long time unsuccessfully with Microsoft products. Little things, such as the entire network of Cisco Systems print servers running on Linux. Success stories like these can be stifled for just so long.

Now some of these Fortune 1000 companies openly support Linux. Many are eschewing other operating systems in favor of Linux for a number of specialized uses. Linux is now being used in embedded systems (Adomo), in palm-top systems (Yopy), in servers, and even in massive parallel processing systems—sometimes called Beowulf clusters—that rival some of the biggest supercomputers in the world. If you look in the list of the “Top 500 Supercomputers (http://netlib2.cs.utk.edu/benchmark/top500/top500.list.html),” you’ll probably find still listed the Avalon Beowulf cluster at the Los Alamos National Laboratory. Finally, Linux can be used where a Real-Time kernel is required. Linux can handle many tasks.

Linux can also run on many different types of hardware. Almost everyone knows that Linux can run on an Intel Pentium processor. But just about anything from a 386 on up is fair game. Linux also runs on Alphas, on some Sun hardware (both 32- and 64-bit systems), on PowerPCs, and a variety of others. Developmental support is also available for the Intel 64-bit architecture (IA64). Some experimental porting has also been done to a VMS VAX. Got an old 32-bit or bigger system lying around gathering dust? Linux might be able to breathe new life into that old hardware.

But don’t let this fool you. Linux isn’t a do-it-all system (yet). Although it scales better than its competition and runs on more different platforms and architectures than any other OS in the world, it still isn’t up to the job in a few areas. Specifically, Linux can’t replace the UNIX “big-iron.” It doesn’t scale well enough to stand up to industrial-strength usage that might be given to some of the big UNIX boxes. One reason is that Linux hasn’t incorporated support for NUMA (an architecture where the access times for different regions of memory from a processor varies according to the “distance” of the memory region from the processor). Although this support is necessary for large multiprocessor systems with gigabytes of RAM memory, it makes small systems excruciatingly slow.
