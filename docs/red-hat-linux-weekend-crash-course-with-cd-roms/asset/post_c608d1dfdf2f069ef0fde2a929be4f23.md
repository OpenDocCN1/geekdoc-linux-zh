
## Credits

**Acquisitions Editors**
Greg Croy
Laura Lewin

**Project Editor**
Terri Varveris

**Technical Editor**
Joseph Riquelme

**Copy Editors**
Victoria Lee
Mildred Sanchez

**Proof Editor**
Neil Romanosky

**Project Coordinators**
Joe Shines
Danette Nurse

**Permissions Editor**
Carmen Krikorian

**Media Development Specialist**
Travis Silvers

**Media Development Coordinator**
Marisa Pearman

**Graphics and Production Specialists**
Robert Bihlmayer
Jude Levinson
Michael Lewis
Victor Pérez-Varela
Ramses Ramírez

**Quality Control Technician**
Dina F Quan

**Book Designer**
Evan Deerfield

**Illustrator**
Danette Nurse

**Proofreading and Indexing**
York Production Services

## About the Author

**Naba Barkakati** is an expert programmer and successful computer-book author who has experience in a wide variety of systems, ranging from MS-DOS and Windows to UNIX and the X Window System. He bought his first personal computer — an IBM PC-AT — in 1984 after graduating with a Ph.D. in electrical engineering from the University of Maryland. While pursuing a full-time career in engineering, Naba dreamed of writing software for the emerging PC software market. As luck would have it, instead of building a software empire like Microsoft, he ended up writing successful computer books.

Over the past 12 years, Naba has written 25 computer books on a number of topics ranging from C++ programming to Linux. He has authored several best-selling titles, such as *The Waite Group's Turbo C++ Bible*, *Object-Oriented Programming in C++*, *X Window System Programming*, *Visual C++ Developer's Guide*, and *Borland C++ 4 Developer's Guide*. His books have been translated into many languages, including Spanish, French, German, Polish, Greek, Italian, Chinese, Japanese, and Korean. Naba's most recent book is the best-selling *Red Hat Linux Secrets, 3rd Edition*, also published by IDG Books.

Naba lives in North Potomac, Maryland, with his wife Leha and their children Ivy, Emily, and Ashley.

This book is dedicated to my wife Leha
and daughters Ivy, Emily, and Ashley.

## Preface

Because of Linux’s increasing popularity, many computer users want to learn it quickly. Red Hat Linux is a dominant Linux distribution that many large businesses use. If you work for an organization that is interested in Red Hat Linux, you need to get up to speed on how to install, configure, use, and manage Red Hat Linux systems. The best way to do so is to install Red Hat Linux and interactively learn its commands and applications. What potential Linux aficionados — beginners to advanced ones alike — need is a well-organized set of sessions that teach them Red Hat Linux over a weekend.

This Red Hat® Linux® Weekend Crash Course™ is such a teaching guide. It provides 30 easy-to-use sessions, each a half an hour long, that gradually build up your Linux skills. Patterned after the IDG Books’ Weekend Crash Course series, these sessions — starting with Red Hat Linux installation on Friday evening and ending with several system administration topics on Sunday afternoon — are designed for you to complete over a weekend.

The crash course’s pace is fast. Each session starts with a “Session Checklist” — a short list of topics that you learn within the session through hands-on exercises. Each session ends with a “Quiz Yourself” section that enables you to test your new skills by answering some questions. For each major part, which corresponds with a time during the weekend, the book also includes Part Review Questions, which cover what was taught in the sessions within that part. You can try answering the Part Review Questions and check your answers in Appendix A.

This book includes CD-ROMs with the latest version of Red Hat Linux. You can install Red Hat Linux by following the instructions in Sessions 1 through 3, and then you can use it throughout the rest of the book.

## What You Need to Get Started

To start the sessions, you need a PC on which you can install Red Hat Linux. The minimum system requirements for the PC are Intel 486 or Pentium-compatible processor, 32 MB RAM, 1 GB of disk space, 3.5-inch floppy drive, and a CD-ROM drive. For some of the other sessions, you need an Ethernet networking card, a modem, and Internet access. You also need a free weekend to go through all the sessions.

## Organization of the Book

Red Hat Linux Weekend Crash Course has 30 sessions, organized into six parts. It also has two appendixes.

Part I: Friday Evening guides you through the steps needed to install Red Hat Linux from this book’s companion CD-ROMs. Assuming that the installation program recognizes most of the hardware, you should be able to finish the installation in an hour or so.

Part II: Saturday Morning focuses on trying out Red Hat Linux quickly, exploring files and directories, learning some Linux commands and text editors, and performing some basic system administration tasks.

Part III: Saturday Afternoon shows you how to set up networking (assuming the PC has an Ethernet card) and connect the Linux PC to the Internet (dial-up PPP, but briefly discusses xDSL and cable modem as well). Some of the lessons show how to use the Linux system in a networked environment as an Internet server (Web, e-mail) or as a Windows file server that uses Samba.

Part IV: Saturday Evening teaches you how to use the GNOME and KDE desktops as well as some of the applications that come bundled with Red Hat Linux.

Part V: Sunday Morning introduces you to various system administration tasks, such as configuring X, learning the Linux boot sequence, installing new software packages from RPM and tar files, building a new kernel, scheduling jobs to run at specific times, and performing system backups.

Part VI: Sunday Afternoon focuses on skills that a Linux system administrator should have. The afternoon starts with a lesson on how to use the programming tools to compile and build a new software package. Then it covers system performance monitoring, security, and obtaining further help.

Appendix A: Answers to Part Reviews provides answers to the Part Review Questions that appear after each of the six parts.

Appendix B: What’s on CD-ROM? describes the contents of the accompanying CD-ROMs.

If you are a new user, you should start with Part I, which covers the installation of Red Hat Linux from the CD-ROMs. Then you can continue sequentially through the sessions. If you already installed Red Hat Linux, skip to Part II on Saturday morning.

## Conventions Used in This Book

Red Hat Linux Weekend Crash Course uses a simple notational style. All listings, filenames, function names, variable names, keywords, and Web addresses are typeset in a monospace font for ease of reading. The first occurrences of new terms and concepts are in italics. Text I direct you to type is in boldface and monospace type combined.

Following the design of the IDG Books' Weekend Crash Course series, I use icons to help you quickly pinpoint useful information. Following is what I had in mind for the icons:

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_12_0.png)

The Note icon marks a general, interesting fact — something that I thought you’d like to know.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_12_1.png)

The Tip icon marks shortcuts or methods that you can follow to make your job easier.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_12_2.png)

The Never icon highlights potential pitfalls. With this icon, I’m telling you: “Watch out! This could hurt your system!”

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_12_3.png)

The Cross-Reference icon points out other sessions in the book that discuss a specific topic — or to specific programs available on the CD-ROMs.

Each session also contains four time-oriented icons that let you know how you are progressing:

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_13_0.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_13_1.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_13_2.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_13_3.png)

## Sidebars

Occasionally, I use sidebars to highlight interesting (but not critical) information. Sidebars explain concepts you may not have encountered before or give a little insight into a related topic. If you’re in a hurry, you can safely skip the sidebars. On the other hand, if you find yourself flipping through the book looking for interesting information, I encourage you to read the sidebars.

## Reach Out

The publisher and I would like your feedback. After you have had a chance to use this book, please take a moment to register this book on the http://my2cents.idgbooks.com Web site. (Details are listed on the my2cents page in the back of the book.)

Also, feel free to contact me directly at:

naba@ieee.org
