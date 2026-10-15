
## Dedication

To Donald Becker, Andrew Tridgell, Adrian Sun, and all the many others who have made Linux networking what it is today.

## Acknowledgments

I’d like to thank acquisitions editor Neil Rowe, development editor Tony Amico, and project coordinator Karen Opal. These are the people who form the buffer between me and all the myriad details of transforming my words into a book. Without their efforts, this book would not be possible.

Jim Westveer served as technical editor on this book, which means he kept me on the straight-and-narrow path where the truth is concerned. If I nonetheless managed to stray, the fault is, of course, mine alone.

Heartfelt thanks go out to David King, who pointed me towards many useful nuggets of information. Adrian Sun also helped clarify several details of operation of the Netatalk package. Any remaining errors are, of course, my own. I’d also like to thank John Kounios, on whose event-related potential (ERP) laboratory computers I learned much of what I present in this book.

In order to write this book, I used the GIMP image manipulation software by Spencer Kimball and Peter Mattis to capture screenshots in Linux, and Bren Tamiilio's ScreenSnatch for Windows screenshots. I used Marko Macek's icccm window manager for controlling onscreen Linux windows (icccm is what you really want if you really like the look of the windows in this book). Of course, I used the Linux kernel by Linus Torvalds and others, along with far too many additional programs and utilities to mention by name.

## Tell Us What You Think!

As the reader of this book, you are our most important critic and commentator. We value your opinion and want to know what we’re doing right, what we could do better, what areas you’d like to see us publish in, and any other words of wisdom you’re willing to pass our way.

As a publisher for Sams, I welcome your comments. You can fax, email, or write me directly to let me know what you did or didn’t like about this book—as well as what we can do to make our books stronger.

Please note that I cannot help you with technical problems related to the topic of this book, and that due to the high volume of mail I receive, I might not be able to reply to every message.

When you write, please be sure to include this book’s title and author as well as your name and phone or fax number. I will carefully review your comments and share them with the author and editors who worked on the book.

Fax: 317.581.4770

Email: opsys@mcp.com

Mail:
Angela Wethington
Publisher
Sams Publishing
201 West 103rd Street
Indianapolis, IN 46290 USA

## Introduction

In the past few years, an initially little-noticed project has been underway. Started at the University of Helsinki in Finland by Linus Torvalds, the Linux kernel was originally a project to reimplement parts of the UNIX operating system on inexpensive PC hardware. It quickly gathered around it the fruit of years of software development for UNIX, especially what has come to be known as open-source software, much of it from Richard Stallman’s Free Software Foundation (FSF). The result of this accretion of software, ranging from the Linux kernel itself to the XFree86 windowing system, the Emacs editor, the gcc C language compiler, and others, is frequently referred to as Linux, though some prefer the term GNU/Linux to spread the credit for the nonkernel utilities, many of which were developed by the FSF’s GNU project. By whatever name it (I use Linux in this book), the result is a very complete UNIX-like operating system that is freely available, stable, and flexible.

One of Linux’s greatest strengths has turned out to be its networking capabilities. Thanks to the efforts of individuals like Donald Becker, Linux supports the vast majority of Ethernet networking cards available today. Because most UNIX programs compile and run on Linux with few or no changes, Linux has been blessed by the wide array of networking tools and utilities available for UNIX. As Linux’s popularity has grown, it has become the development platform of choice for many networking tool authors. Tools like Samba would probably exist without Linux, but they might not be quite as mature or popular as they are.

This book is designed to help you explore the world of Linux networking. Actually, it might be more accurate to say that this book is designed to help you explore one continent in the world of Linux networking. A thorough description of Linux networking is well beyond the scope of a single book. This book focuses upon those networking features of most interest in a small office/home office (SOHO) environment—file sharing, printer sharing, and assorted methods of connecting to the Internet, to name the main topics. Other books in the Sams Linux networking series explore other continents in the world of Linux networking.

## Who Should Buy This Book

This book is written with a person possessing moderate to advanced Linux knowledge in mind. I expect the reader has relatively little knowledge of the details of using Samba, Netatalk, IP masquerading, and the other topics covered in this book. You should be familiar with basic Linux operations and principles, such as user accounts, command line shells, and operation of the X Window System. You might or might not be familiar with Linux’s model of system administration, such as the locations of configuration files and use of tools such as linuxconf. If you’re more of a Linux “newbie,” you should still be able to use this book, but you should read it in conjunction with a basic text on Linux operations, such as Pitts & Ball’s Red Hat Linux 6 Unleashed, from Sams Publishing.
