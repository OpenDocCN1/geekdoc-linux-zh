
## What You Need to Use This Book

Although it’s not essential, a working knowledge of DOS will help you grasp the concepts in this book. You don’t need to be a hacker to use Linux, but it is an operating system, and operating systems can be technically challenging. Still, the book aims to provide enough background for most people to tackle just about any Linux problem they may encounter.

## A Really Brief History of Unix

Sometime in the mid 1960s, a bunch of geeks at AT&T’s Bell Labs decided it would be fun to create a new operating system called Multics. (This was no small task, because computers at the time were about the size of a football field and two stories high.) Multics fizzled in 1969 when Bell cut the cord, but some of the geeks continued work on what became known as UNIX; and it became wildly popular inside AT&T.

Since AT&T was not allowed to sell computer software at the time, it gave away UNIX (complete with source code) to any educational institution. AT&T produced new versions of UNIX called System III and System V in the early 1980s, but all the while, geeks at the University of California at Berkeley and other places were busy hacking away on their own versions of Unix based on the AT&T code. Some cross-pollination did occur, but there are still significant differences between the Berkeley (commonly called BSD Unix) and AT&T flavors. In the early 1990s, AT&T sold UNIX to Novell, which was bought by Digital Equipment Corporation, which sold it to SCO (Santa Cruz Operation), which markets it as UNIXWare.

Today, there are now lots of Unix variants sold or given away by many different companies and universities. While these various flavors can make it difficult to write portable software, efforts to standardize Unix (two of the more notable ones being POSIX and COSE) offer hope for greater compatibility in the future.

Like any operating system, Unix has some cryptic commands and less-than-intuitive aspects. (Three of the most important Unix commands have the peculiar names cat, grep, and awk.) Either serious hallucinogens or a warped sense of humor came into play at some point in the creation of Unix. I don’t let this bother me, though, taking comfort in my favorite platitude: “Unix was written by geeks on drugs.” Seriously, though, Unix is really no more difficult to learn than DOS or Windows—it’s just different.

## Uh, What’s an Operating System?

For a computer to do anything useful, it needs both application software (programs you use) and an operating system (programs the computer uses). The operating system sits between the physical hardware that makes up a computer (the monitor, keyboard, CPU, hard drive, and so forth) and the end-user software that people use to process documents, play games, and all that good stuff.

My brother Tom and I are both into computers. We’re computer programmers by trade, but I’m quick to point out that we produce very different kinds of software. The difference, as I like to explain it, is this: I write software for people; Tom writes software for computers.

We commonly think of the CPU as the brain of a computer, but in reality, it can’t do much besides crunch numbers and move data around in the computer’s memory. The job of the operating system (OS) is twofold:

- 1. To work with computer hardware to process user requests by
  - interpreting keystrokes from the keyboard,
  - displaying images on the screen,
  - storing files on the hard disk,
  - sending documents to a printer,
  - communicating over a modem.
- 2. To manage the application software’s use of memory (RAM) and processor time.

If you’ve used a multitasking environment like Windows or a multi-user mainframe system, you’ve seen the concept of “time-slicing” in action. While your computer has only one CPU, which can do only one thing at a time, the OS can make it seem like several people or programs are using the CPU simultaneously. Similarly, even though the real memory (RAM) is shared by all running applications, the OS can make it seem like you have it all at your disposal, all the time, by sharing it between applications—using a technique called paging.

The OS time-slices giving one user or application exclusive use of the hardware for a brief instant, and then doing the same for the next user or application. On systems with adequate horsepower, this approach works so that you never even know about that little game of round-robin going on behind the scenes. On a wimpy computer or a mainframe with too many users, it’s toe-tappin’ time for everybody.

## MY LAWYER MADE ME DO IT

*Red Hat* is a registered trademark and the Red Hat Shadow Man logo, RPM, the RPM logo, and Glint are trademarks of Red Hat Software, Inc. *Linux* is a registered trademark of Linus Torvalds. *Motif* and *UNIX* are registered trademarks of The Open Group. *Netscape* is a registered trademark of Netscape Communications Corporation in the United States and other countries. *TrueType* is a registered trademark of Apple Computer, Inc. *Windows* is a registered trademark of Microsoft Corporation.

All other trademarks and copyrights referred to are the property of their respective owners. Your mileage may vary. No warranty expressed or implied. Objects in mirror are closer than they appear. Consult your physician before using this product.

## UPDATES TO THIS BOOK

Changes happen fast in the Linux world, but we’ll do our best to keep you posted about anything that affects the content of this book after press time. Visit http://www.nostarch.com/rhl_updates.htm for more information.

## WHERE AM I?

In this introduction to Linux, you’ve learned the basic tasks of an operating system and how it differs from application software. You’re now an expert on Unix history, you understand that Linux is a version of Unix for ordinary PCs, and you can even pronounce the name correctly. You don’t have a clue about hardware requirements or installation, but that’s coming next.
