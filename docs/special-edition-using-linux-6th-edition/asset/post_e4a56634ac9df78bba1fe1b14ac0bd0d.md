
But that leaves many areas where Linux can still make work and grow. The home and business desktop is one area where Linux growth is set to explode in the next few years. With every new software product that’s ported to Linux, that’s one less reason for users not to switch their desktops. When the few remaining holdouts do port to Linux, expect to see the desktop arena start to change dramatically.

Now, products abound for Linux, sufficient products for almost any need, in almost any category you can think of: office suites (word processing, spreadsheets, databases, personal information managers, email), games, educational software, SQL servers, you name it.

So what has held Linux back from the home and desktop market to date? For one thing, the average user will explore exactly what comes on the computer system he or she brings home from the local computer shop or Electronics World. These users know very little except that if they turn the system on and click whatever button looks likely to offer them something, they might be able to find a game or a word processor. They are unaware that choices exist.

More specifically, they are unaware that Linux is an operating system (*What’s an operating system?*) that could be installed and used on their new computer (*You can do that? Put another operating system on a computer? How?*). The OEMs up to now have been no friend of Linux either. Until it became clear that Microsoft was going to lose the trial on charges of being a monopoly, even the biggest OEMs feared Microsoft enough to only offer one operating system. This too is changing, albeit slowly.

Several large OEMs (IBM and Dell to name two) now offer servers with Linux, and even desktop machines can be ordered this way (though with desktops and laptops you have to know to ask for it).

Still, Linux rates as one of the fastest growing operating systems in the world for one reason: It works. There’s a lot to be said for marketing hype. It can confuse and bewilder. But after the hype is revealed for what it is, users choose what works.

## A WORD ABOUT HARDWARE

Before you rush out and buy Linux to install on your system, you might want to take some time to see whether your distribution of choice will support, out of the box, the hardware that you have.

One of the most frustrating things for newcomers to Linux is that in all the excitement of trying out this great new operating system, they forget to see whether the hardware they intend to use it on is supported.

Windows NT cannot be installed on all hardware; some is just not supported. Ditto for nearly every operating system in the world. Not all hardware vendors support Linux; some disdain this operating system, so expect no support from them. Also expect either no drivers, or drivers that work only marginally well. Older hardware is more likely to have the required support. Newer hardware might or might not, depending on the particular manufacturer. So look before you buy.

## ABOUT THIS BOOK

This edition of *Special Edition Using Linux* actually started life as the second edition of *Special Edition Using Caldera OpenLinux*. As such, this book is somewhat Caldera-centric. But the authors have taken pains to see that Debian and Red Hat were included when the plans for this text changed.

That doesn’t mean you need to run Caldera or Debian or Red Hat to get something out of this book. In fact, it almost doesn’t matter what Linux distribution you choose. This book will provide insights into your own particular distribution choice. So whether you use SuSE, Mandrake, Corel, or even Slackware, this text has something for you. In fact, over 90% of this text is distribution non-specific, but decidedly Linux-centric. Covering specifics of all the distributions on the market would be a difficult task, and in the end, would only result in a lot of text repeating itself.

As you’ll see while reading through this book, only a few things differentiate Linux distributions: installation, system administration, software package management, software package selection, system initialization, and philosophical bent. The kernel is (for all intents and purposes) the same. The major pieces are the same. Most software packages are exactly the same. So don’t fret the small stuff; look to see what’s different where, and see how it still all works the same.

This book is written to the not-yet-released 2.4.x kernel, and the latest unstable software snapshots available. So what you see might not be exactly what is described in the text, but should be valuable to you for a number of insights for the next few years (at least until v 2.6 or 3.0 comes out).

By the time this book is on the shelves, however, you should be able to judge how well the authors predicted the future, even though the future looked fairly stable while it was being written about.

Also for the first time, *Special Edition Using Linux* is published sans CD-ROMs. This decision was made so as not to do a disservice to either the book or its audience by providing something that wasn’t ready for prime time (only Caldera’s Linux Technology Preview was released with the 2.4.0test3 kernel, a kernel which is significantly different from any of the test6 and beyond kernels) or wasn’t completely in step with the book (that is, a kernel version 2.2.x).

Additionally, the authors are committed to maintaining a Web site to update material in this book to make it as useful as possible throughout the life of the 2.4.x kernel.

## WHO SHOULD USE THIS BOOK?

Anyone who is contemplating installing Linux for the first time should read through this book and keep it handy after their install. Any new Linux systems administrators or UNIX administrators who are not considered gurus or wizards will benefit from using this book.

This book is aimed at the beginning, intermediate, and in some cases, advanced systems administrators who need a reference to most aspects of running and administering Linux.

## WHO SHOULD NOT USE THIS BOOK?

If you are a Linux kernel hacker or a UNIX guru, this book might not be up to your expectations. This book is a great resource if you want to know more about Linux and UNIX but have never been involved with either operating system as anything more than a user.

This book will not go into a fairly large number of extremely complex, but mostly “niche” topics, such as the use of iproute2 to do bandwidth limiting, ingress and egress queuing, and the like. Nor will it cover security in any great detail. Some of the topics covered in the book also have conveniently ignored aspects considered either too advanced or too detailed to be covered completely, such as network netmasks that don’t correspond to the /nn designations. You will find books devoted to the subject of networking, which here has dedicated only one, albeit large, chapter, as well as to a number of other specialized areas of knowledge covered for basic and intermediate orientation and reference in this book.

However, even if you know how to install Linux and maneuver around in UNIX, you might still find this book of use, particularly if you are only a UNIX user and have never had the chance to perform system administration tasks. Several sections of the book explain the finer points of system administration and how to maintain a Linux/UNIX system. Typically, a normal UNIX user does not perform these system administration tasks, but with Linux, you are the system administrator, free to do whatever you want to do!

Now, if you don’t have a clue what a computer is or what a floppy disk looks like, you might want to brush up on some computer basics before tackling Linux. Linux isn’t for everyone, but there’s a reason why it shouldn’t be.

## CONVENTIONS USED IN THIS BOOK

This book uses several special conventions that you need to become familiar with. These conventions are listed here for your reference:

- Linux is a *case-sensitive* operating system; that means when this book instructs you to type something at a command or shell prompt, you must type exactly what appears in the book, exactly as it is capitalized.
- This book uses a `monospaced typeface` for Linux commands to set them off from standard text.
- If you’re instructed to type something, what you are to type also appears in monospaced text. For example, if the book gives the instruction “Enter cat,” you must press the letters *c*, *a*, and *t* and then press the Enter key.
