
## E COPYRIGHT INFORMATION 1055

## F WHAT'S ON THE CD-ROM? 1061

Award-Winning Operating System ...................................................................1062

Desktop Environment ...............................................................................1062

Internet Server ................................................................................................1062

Learning Platform .......................................................................................1062

About the Software .....................................................................................1062

# About the Author

Dr. Tim Parker has written more than 40 books covering many aspects of the computer business. He is the technical editor of SCO World Magazine, as well as a frequent contributor to dozens of magazines, including UNIX Review, Canadian Computer Reseller, UNIQUE: The UNIX Systems Information Source, Windows NT Systems, and others. Dr. Parker is the most widely published UNIX author in the world. When not putting up with temperamental computers, he spends his time flying, diving, and riding his favorite motorcycle.

# Dedication

This one is for Yvonne. What more can I say? Amor vincit omnia.

# Acknowledgments

As with the previous versions of Linux Unleashed, this book has been superbly managed by the fine folks at Sams. Both Jane Brownlow and Mark Cierzniak worked with me to produce another tome we are all proud of. Thanks to the technical reviewers who took the time to make excellent suggestions for improvements and to the copy editors who made sure every sentence made sense. Without all these people working under very tight deadlines, we would have a much weaker book.

Thanks to the staff at Caldera for providing not only multiple versions of their Linux distribution, but also several applications for inclusion. Thanks also to Lone Star and Cactus for their Lone-Tar product. On a personal level, thanks to my parents for tolerating yet another few months when I couldn't visit. Thanks to “the boys” for the delightful deviations on Thursday nights. Finally, thanks to Yvonne for understanding why I had to, yet again, spend my mornings, days, and evenings in front of my computers instead of with her.

## Tell Us What You Think!

As the reader of this book, you are our most important critic and commentator. We value your opinion and want to know what we’re doing right, what we could do better, what areas you’d like to see us publish in, and any other words of wisdom you’re willing to pass our way.

As the Executive Editor for the Operating Systems team at Macmillan Computer Publishing, I welcome your comments. You can fax, email, or write me directly to let me know what you did or didn’t like about this book—as well as what we can do to make our books stronger.

*Please note that I cannot help you with technical problems related to the topic of this book, and that due to the high volume of mail I receive, I might not be able to reply to every message.*

When you write, please be sure to include this book’s title and author’s name, as well as your name and phone or fax number. I will carefully review your comments and share them with the author and editors who worked on the book.

Fax: 317-581-4663
Email: opsys@mcp.com
Mail: Executive Editor
Operating Systems
Macmillan Computer Publishing
201 West 103rd Street
Indianapolis, IN 46290 USA

# INTRODUCTION

## PART I

## In This Part

- Introduction to Linux 5
- Types of Linux 25
- Installing Linux 39
- Using LILO 67
- Wrapping Up the Installation 89

## Introduction to Linux

*by Tim Parker*

### In This Chapter

- What is Linux? 6
- Linux’s history 9
- What Linux can do for you 10
- What you need to run Linux 12
- Minimum system requirements 12
- Copyrights 18
- Getting help 19
- Usenet newsgroups 20
- What’s in this book? 22

You've seen dozens of books about it. You've read magazine articles about it. There are Usenet newsgroups with hundred of messages a day, CD-ROMs of Linux archives sold by the thousands, and even more Windows users wandering around trying to figure out what to make of this Linux phenomenon. Despite the popularity of this operating system, there are still thousands, if not millions, of users who are curious about Linux but are afraid to take the first steps: installing and playing with the system. That's what this book is intended to help with. We'll guide you step-by-step through the installation procedure, show you how to use Linux, and generally introduce you to this wonderful world of UNIX.

Before we start, though, a quick word on pronouncing “Linux.” There are two schools of thought about the *i* sound in “Linux”; because Linux is similar to UNIX and was originally developed by a programmer with the first name Linus, many assume that the long *i*, as in “line-ucks,” is the correct pronunciation. On the other hand, Linux was actually developed to replace a UNIX workload called Minix (with a short *i*, so the rest of the Linux community calls the operating system “lih-nixes.” Which is correct? The original developers use the latter pronunciation, while most North Americans prefer the former. Choose whichever you prefer. Either way, we know what you mean.

# What Is Linux?

Linux, for those who haven't figured it out by now, is a freely distributed multitasking multiuser operating system that behaves like UNIX. Linux was designed specifically for the PC (Intel CPU) platform and takes advantage of its architecture to give you performance similar to high-end UNIX workstations. A number of ports of Linux to other hardware platforms have also appeared, and they work much like the PC version that we'll concentrate on here.

To begin, let's look at the Linux operating system as a package. When you install Linux, what do you get? Here's a quick list, most of which is expanded in future chapters.

## Linux's Kernel

Linux is a complete multitasking, multiuser operating system that behaves like the UNIX operating system in terms of kernel behavior and peripheral support. Linux has all the features of UNIX, plus several recent extensions that add new versatility to Linux. All source code for Linux and its utilities is freely available.

The Linux kernel was originally developed for the Intel 80386 CPU's protected mode. The 80386 was originally designed with multitasking in mind (despite the fact that most
