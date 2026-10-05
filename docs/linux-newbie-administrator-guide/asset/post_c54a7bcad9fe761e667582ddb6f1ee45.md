
Slackware seems to be among "cutting-edge hackers" who like being close to the operating system and upgrade their kernel every other day--we did not use it so this is hearsay. S.uSE distribution is very popular in Europe. It likely looks German-solid, general-purpose distro with an easy setup and excellent reputation. Another well-known and respected distribution is Caldera, said to be aiming at corporate users--which has many faults, Mandrake distribution is a RedHat clone which is updated more often than the pedigree RedHat (RedHat tends to update less often so not to proliferate too many versions). Mandrake seems to be very popular. They are "localized" versions of Linux for specific countries or languages (Korean, Japanese)...they likely contain on default all the hacks and that the users in these countries want to see.

There are also "special purpose" distributions, e.g. the "real-time" editions of Linux (might be useful if you are for automation, robotics, etc.), very small distros (could be good for the next-generation CD/MP3 player or if you like the idea of running Linux from a small floppy), parallel computing and clustering systems (might be great if you plan to do your own whatever :-); here the differences will be larger, but these distributions are not meant to be "general purpose". As a newbie, you don't want to start with any of these, although you might be tempted to. They surely show Linux strength and viability--it runs on you as computer clusters that make the fastest systems in the world.

The distribution you need is of course to specify the hardware you have. For your PC hardware containing a Intel 386 processor, or 486, or Pentium, or Cyrix, or K6, or similar, you need the binary distribution "Intel" or "386". [Unless you are prepared to start with your compilation of the Linux source code, which is not typical for a newbie :-] This happens because there are binary distribution for other platforms too (PowerPC, Alpha, and perhaps a dozen more)--don't get you for your PC clone, surely they will not work.

In short, newbies get confused with the multiple Linux distributions, there are reasons to have different distributions. This should be viewed as a Linux strength rather than weakness.

This guide concentrates on RedHat 5.2, 6.0 and 6.1 on the (Intel) platform. Many of the answers will work on other distributions or platforms, but we did not try to.

## 1.2 What are the Linux hardware requirements?

Out-of-box Linux runs on a 386-based PC with 8 MB of memory, but a low-end computer is practical for text-only applications (no X-Windows). A 486 with 16 MB memory and 600 MB free (unpartitioned) hard drives will do to work with X-Windows. My 586-900 MHz with 64 MB of memory flies us. My Pentium 2 237 MHz with 64 MB of memory is a complete pleasure with an almost instantaneous response even when running many large applications concurrently. My 486-32 MHz with 8 MB of memory and 1 GB hard drive has too little memory to run adequately stand-alone under GUI, but is useful in my home network environment (a 486-class machine performs just adequately stand-alone if it has at least 16 MB of memory). My old portable 386-SX-20 MHz Toshiba with 9 MB and 120 MB hard drive runs "legacy applications" under MS Windows 3.11 and connects to our home network and is thus still useful. We tried Debian on this Toshiba too, and it runs fine in text mode.

If you are willing to jump through a few extra hoops, you should be able to run Linux on a little as 4 MB of memory, but this is probably not worth the effort for the general purpose home Linux machine. I would say: get at least 16 MB of memory, and if possible 32 or 64 MB --memory can make a difference when running concurrently several GUI applications. Memory is cheap these days.

Networking is where Linux shines, so considering 10-base T cards—they are not very expensive and will be perfect to connect your two or more computers together. Also, look around for old cards which Windows deems obsolete—they can be bought for a low price and will work fine under Linux. To connect just two computers, a cross-over cable for direct Ethernet-card to Ethernet connection is sufficient. To connect more than 2 computers, you need a hub (~US$30 to US$80) and normal (not cross-over) cables. If you have Ethernet cards, you may also consider installing than 1 Ethernet card on a computer, use direct connections using the cross-over cables, and save the expense of a . The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub). The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

Here is another suggestion on setting up a kind of network, order type, which uses coaxial cables. For nothing is necessary. This networking scheme is older, but can be assembled using cards and parts that are also available for free:

(edited for Space) From: John.Edwards@brunel.ac.uk Subject: Linux Guide-a-suggestion

Many 100Mbps network cards (and some ones as well) have a BNC connector and you can usually pick up old co-axial cabling when companies upgrade to UTP. Add a T piece for each machine and a 50-ohm terminator at each end (about 1 pound or $1,50 each)

Disadvantages:
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.
- Many 100Mbps network cards (and some ones as well) have a BNC connector and you can usually pick up old co-axial cabling when companies upgrade to UTP.
- Add a T piece for each machine and a 50-ohm terminator at each end (about 1 pound or $1,50 each)
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

- is more is
- and you don't see
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

- is more is
- and you don't see
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

- is more is
- and you don't see
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

- is more is
- and you don't see
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

- is more is
- and you don't see
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

- is more is
- and you don't see
- The 10-baseT system uses "giant phone" connectors and all machines are connected to one box (called the hub).
- The hub has an extra connection (called "uplink") which you will use if you ever have a permanent connection to the outside world.

For more detail see page of 

Another area of potential problem is the video card. If you have a recent "cutting edge" 3D or uncommon, you may want to check its compatibility at http://www.Xfree8.org.

So the short answer is, in all likelihood your PC will run Linux with no problems. You don't invest much when trying Linux, so the easiest way to make sure is to attempt an installation on your hardware.

When purchasing new hardware, ask your supplier if the hardware is supported under Linux or consider a system with Linux preinstalled. Not too many suppliers offer you yet (plan to), but you can get one from a smaller vendor.

## 1.3 Will my hardware work?

Not every piece of hardware is supported in Linux, but most are. This applies to SCSI adapters, CDROMs, writable and rewritable, video cards, mice, printers, network cards, scanners, drives, etc.

The most notable exceptions are the socalled Winmodels. Avoid these fire-like—maybe $5 less than externalems are never Windows models so if doubt, purchase an external modem (you can order it for $19).

## 1.4 How do I download Linux?

Do yourself a favor and do not download Linux, get an installation instead. Linux can be downloaded completely from the Internet, but it is a large and sophisticated operating system. The download will take hours or days of download time and you will probably encounter problems trying to stitch the downloaded pieces together.
