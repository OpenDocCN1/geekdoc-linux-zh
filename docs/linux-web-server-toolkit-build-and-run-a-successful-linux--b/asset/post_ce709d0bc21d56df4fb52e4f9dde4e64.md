
## Chapter 2: Using Linux for Your Web Server

## Understanding “Free” Software

People often misconstrue what free software means. Definitions of common terms follow, but be careful – licensing is always determined by the creators. And don't believe the terms you read until you check the actual software license. (Oh, and use your attorney's definitions for your contracts, mine.)

Public Domain: This means “owned by everyone.” Software in the public domain can be copied freely and used as the basis for any work without royalties or the need to provide the new code to anyone. Public domain software can be altered or redistributed under any product name, without even acknowledging the original source. Once an author places a piece of software in the public domain, it cannot be removed from the public domain by anyone.

Shareware: An author can create a piece of software and distribute it freely on the honor-system condition that users will send a small payment if they like the software and continue using it. Shareware is a try-before-you-buy system – authors hope to reap a monetary reward for their efforts.

Shareware has fallen out of favor lately, probably because of changing distribution methods – BBS systems are not so popular as the Internet – and the increase in truly free software and GPL software.

Free Software or Freeware: An author can distribute software by simply giving it away. The legal difference between this and placing it in the public domain is vague, though the author retains the copyright ownership even if the software is announced to be free for everyone to use, copy, resell, and so on.

Freeware is like GPL software, but authors do not seek to propagate software development through a larger community of interested parties. Freeware also doesn't have to include source code – plus to developers who don't want their techniques exposed to all see.

GPL: From the Free Software Foundation, GPL software includes source code, can be redistributed for money and without specific permission, and can be modified by anyone. Any modifications, however, must be provided to everyone (this is sometimes called the “virus clause,” because any work incorporating any software distributed by the copyright holder under the GPL is “infected” by the same requirements as the original work).

Other free distribution licenses: Many individuals and organizations create software that can be redistributed for free, subject to certain conditions outlined in their licenses. These conditions generally include keeping the license statement and copyright information intact, and not disassembling and modifying the software. Free-distribution licenses often require that you obtain permission before distributing the software. Many universities use this type of license to propagate their creations while affording themselves a little protection.

## Linux Web Server Toolkit

You can buy one of these Linux distributions on a CD-ROM or download it from an Internet FTP site. Because of the GPL, the Linux distribution is actually free; when you buy a CD-ROM, you are buying either a packaging service, or more frequently nowadays, the brand name that you associate with features and reliability from the company that assembles the free components and maintains the ongoing development of Linux distribution. The CD-ROM costs money—the GPL does not prohibit charging the software—but anyone who buys a CD-ROM of GPL software is free to duplicate it and sell the software (but don't try this with non-CD-ROMs!).

You need to be aware, that most Linux distributions use software that is distributed under a variety of licenses, including some for which the Linux provider obtained specific permission to distribute the code on CD-ROM. Because of this, it's usually best not to duplicate or redistribute any Linux distribution without research into the ownership of its components.

## Caldera and Linux

An interesting thing happened to Linux in 1994. A company named Caldera took the standard, free Linux system and bundled in commercial, nonfree pieces to what was missing from Linux, such as support for Novell NetWare. In the process, Caldera created a complete, integrated operating system for commercial use. Because it could charge more for this product than a simple CD-ROM of a Linux distribution, Caldera began to establish a true, commercial presence for the Linux technology. The Caldera Web page is shown in Figure 2-1.

![](img/e01f1106dd2902613fa07890c8baa7e6_59_0.png)

Figure 2-1: The Caldera home page shows some of Caldera's Linux solutions for businesses. *

In doing this, Caldera overcame the flawed business model of making Linux CD-ROM products that anyone can copy and resell, effectively driving the price of undifferentiated products down to the hard cost of duplicating a CD-ROM. Some other Linux companies followed Caldera's lead and now add value to their Linux systems and work to enter the commercial, business market.

The Caldera OpenLinux CD-ROM included with this book is the distributable portion of the Caldera Linux system, OpenLinux. It is the core for other Caldera Linux products and contains all the software you need to create a complete Web site. We talk more about that in Chapter 3; for now, I focus on why you should use Linux for your Web server.

## Key Benefits of Linux

The remaining sections of this chapter describe the key benefits of Linux that make it such a strong contender as a server platform. The feature descriptions may be just what you need to convince any skeptics in your organization about the value of Linux.

## Low Cost

You can get linux for nothing—that is, nothing but a fair amount of time sitting at your computer. Most Linux distributions are available for free download from an FTP site. Most are also between 200 and 600MB. With your 14.4K model, let's say... that won't take more than a lifetime. So you can see why the packaging of Linux CD-ROMs has been a popular business.

### But even if you pay for Linux

Even the most expensive versions of Linux, as Caldera's top-of-the-line OpenLinux product, are a bargain compared to similar offerings from other system vendors. With Linux, you always get more because no one had to pay a staff of developers for five years to create the operating system.

In addition, the hardware requirements of Linux make it an inexpensive system to operate. The OpenLinux CD-ROM included with this book can run an acceptable small Web server, with a hundred HTML pages and 1,000 hours per day, on an Intel 386 with a 200MB hard disk and 8MB of RAM. See what your copy of Windows NT can do with that system. Linux supports hundreds of diverse hardware types and peripherals, but you never need the high-end equipment to get a running system. You can use ATM or FDDI cards, but you can also use $29 Ethernet cards.

## High Performance

UNIX has been around for a long time – more than 30 years. In that time it has been around for more than 30 years. In that time it has been added to, passed around, and fixed by a dozen companies. In that time it has been around for more than 30 years. In that time it has been added to, passed around, and fixed by a dozen companies. In that time it has been around for more than 30 years. In that time it has been added to, passed around, and fixed by a dozen companies. In that time it has been around for more than 30 years. In that time it has been added to, passed around, and fixed by a dozen companies. In that time it has been around for more than 30 years. In that time it has been added to, passed around, and fixed by a dozen companies. In that time it has been around for more than 30 years. In that time it has been added to, passed around, and fixed by a dozen companies.

The result is that Linux has a small, fast kernel. It enables features that UNIX systems have, like true multitasking (Linux), multiuser access, virtual memory, and networking.

Comparing Linux to other systems for speed remains mostly anecdotal at this point, because few research studies have been done on Linux, but it is starting to appear as an option on UNIX systems.

One real estate office decided to use Windows NT for its server. I've seen a Pentium Pro 200 with 512MB of RAM handle more than 60,000 requests per day for a large company.

In another set of tests using BYTE magazine's benchmarking software, Linux running on a Pentium 133MHz scored 22, Sun SPARC 50MHz with dual CPU, normally considered to be much faster than Intel hardware, scored 14.1, and HP 9000 755 (RISC processor-based system) scored 14.1. Visit this URL for details: http://www.silkroad.com/linux-bm.html.

## Stability

What do I mean when I say Linux is stable? Basically, it never crashes. Linux goes. Most users of Windows NT or SCO UNIX are not surprised to have to reboot their systems every week or two to keep things running; a well-configured Linux system seems never to go. One Calder system in Canada has been running 24 hours per day, seven days per week for more than 400 days without going down.

A study by the University of Wisconsin adds strength to the Linux argument. In a series of tests, each of the major UNIX vendors' products were 'beaten' with random data to see how they performed under stress. Compared to UNIX systems from IBM, SCI, HP, Sun, and others, Linux had the fewest utility crashes.

During testing of numerous system utilities in 1995, Linux hung or crashed in only 9 percent of tests, compared to 18 to 43 percent for commercial UNIX systems. Visit this URL for full details and a copy of the research report: http://www.cs.wisc.edu/-bart/fuzz/fuzz.html.

For ultimate flexibility, Linux includes full source code. No Linux user is held captive by a software company; there is an expert nearby—on the Internet or in the next cubicle—who can resolve a problem, because all the code is available for review and alteration.
