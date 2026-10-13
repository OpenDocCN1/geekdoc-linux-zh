
## Introduction

SUSE Linux is an increasingly popular Linux distribution that competes head-on with Red Hat’s Linux versions. SUSE Linux’s fortunes have been on the rise following Novell’s acquisition of Germany’s SUSE Linux AG and the recent initiation of the openSUSE project (www.opensuse.org) — an open source project, sponsored by Novell, in which a community of developers, end users, and other open source enthusiasts can participate and continue to evolve SUSE Linux. The recent migration to the openSUSE community-based development model has generated a distinct “buzz” around SUSE Linux as the up-and-coming Linux distribution for everyone from home users to enterprise servers.

A significant factor in SUSE Linux’s increasing popularity is that unlike its competitor Red Hat’s singular focus on the enterprise market, Novell continues to address both the enterprise market and Linux enthusiasts. Specifically, the SUSE Linux open source software (OSS) is aimed at small-office/home-office users as well as those wishing to experiment with the SUSE Linux as their desktop system. The commercial version of SUSE Linux is sold as a boxed set through distributors as well as online stores. SUSE Linux is a complete Linux distribution, suitable for small office/home office or even an enterprise. This book includes a DVD with SUSE Linux 10 OSS, with everything you need to use it as a personal desktop system.

If you are starting out with SUSE Linux, you need a beginner’s guide that not only gets you going with the installation and setup of SUSE Linux, but also shows you how to use all the tools that come with your desktop. That’s why I wrote *SUSE Linux 10 For Dummies* in plain English, using a breezy style, that quickly gets to the step-by-step instructions for accomplishing a task, be it installing a printer or crafting a memo with OpenOffice.org Writer. My goal is to minimize confusion and keep things as simple as possible. I present the essential steps for specific tasks, but avoid inundating you with too many details.

### About This Book

*SUSE Linux 10 For Dummies* is a beginner’s guide for the upcoming SUSE Linux distribution. The approach to the subject matter and the writing style is that of the successful *For Dummies* series. The focus is on introducing you to the SUSE Linux desktop with all the GUI tools, including the office productivity suite (OpenOffice.org) and multimedia applications (audio player, digital camera, CD burning, image editing, and so on). I include a chapter on connecting to the Internet using cable/DSL modems and setting up a basic home network because these have become necessities for anyone who has more than one PC and, especially, for those who plan to run SUSE Linux on a PC. I also include a part that introduces the basics of routine system administration, how to add and update software, and how to tighten up the system’s security.

Here are some of the things that this book shows you how to do:

- Install and configure SUSE Linux from the DVD-ROM included with the book.
- Connect the SUSE Linux system to the Internet through a DSL or cable modem.
- Set up dialup networking.
- Add a wireless Ethernet to your existing network.
- Get tips, techniques, and shortcuts for various uses of SUSE Linux, such as:
    - Using the OpenOffice.org office suite
    - Browsing the Linux file system
    - Using Linux commands
    - Using multimedia applications
- Understand the basics of system and network security.
- Perform system administration tasks.

### Conventions Used in This Book

I use a simple notational style in this book. All listings, filenames, commands, and keywords are typeset in a monospace font for ease of reading. I italicize the first occurrences of new terms and concepts, and then provide a definition right there. I show typed commands in boldface. The output of commands and any listing of files are shown in a monospace font.

### What You Don’t Have to Read

Each chapter zeros in on a specific task area — such as using the Internet or preparing documents with OpenOffice.org — and then provides hands-on instructions on how to perform a series of related tasks. You can jump right to a section and read about a specific task. You don’t have to read anything but the few paragraphs or the list of steps that relate to your question. Use the Table of Contents or the index to locate the pages relevant to your question.

You can safely ignore text next to the Technical Stuff icons as well as the sidebars. However, if you are the kind who likes to know some of the hidden details of how Linux works, by all means, dig in to the Technical Stuff and the sidebars.

### Who Are You?

I assume that you are somewhat familiar with a PC — you know how to turn it on and off and you have dabbled a bit with Windows. Considering that most new PCs come preloaded with Windows, this assumption is safe, right? And I assume that you know how to use some of the Windows applications such as Microsoft Office. Most of all, you want to either experiment with or switch to SUSE Linux as your desktop of choice.

When installing SUSE Linux on your PC, you may want to retain your Windows 2000 or Windows XP installations. I assume that you are willing to accept the risk that when you try to install SUSE Linux, some things may not quite work. Problems can happen if you have some uncommon types of hardware. If you are afraid of ruining your system, try finding a slightly older spare Pentium PC that you can sacrifice and then install Linux on that PC.

### How This Book Is Organized

*SUSE Linux 10 For Dummies* contains 23 chapters organized into five parts. The book’s organization is that of a typical *For Dummies* title that covers an operating system such as SUSE Linux where the reader is expected to install the software and then learn to use it. The five parts cover installation and setup, test driving the system to learn the ropes, using the system to do productive work, learning to be a budding system administrator, and the mandatory “Part of Tens.” Here’s a quick overview of the five parts and the appendix:

- **Part I: Getting to Know SUSE** introduces the reader to SUSE Linux, provides step-by-step installation instructions, and explains what happens when you start the system for the first time.
- **Part II: Test-Driving SUSE** is about getting started with SUSE Linux — how to use the desktop and the file manager, how to connect to the Internet (and set up a home network) — and figuring out what else is there to play with.
- **Part III: Doing Stuff with SUSE** turns to doing day-to-day things with the SUSE Linux system such as browsing the Web, reading e-mail and newsgroups and making IP phone calls, using the OpenOffice.org office suite and some multimedia applications, and, finally, working with the command line shell.
- **Part IV: Becoming a SUSE Wizard** includes chapters on the basic system administration and security. In particular, Part IV explains how to add new software and keep the SUSE system up to date with the YaST (Yet another Setup Tool) installation/configuration tool and YaST Online Update (YOU).
- **Part V: The Part of Tens** is the standard Part of Tens with chapters that present ten frequently asked questions about SUSE, ten best things about SUSE, ten great SUSE-related Web sites, and ten most commonly used SUSE Linux commands.
- **Appendix: About the DVD-ROM** summarizes the contents of the book’s companion DVD-ROM.

### What's on the DVD?

The DVD contains SUSE Linux 10 from the openSUSE project. You may use the DVD in accordance with the license agreements accompanying the software. To find out more about the contents of the DVD, please consult the appendix.

### Icons Used in This Book

Following the time-honored tradition of the *For Dummies* series, I use icons to help you quickly pinpoint useful information. The icons include the following:

![](img/b7e91b81e0d84c8a5261ee14a48991b2_20_0.png)

The Remember icon marks a general interesting fact — something that I think you might want to know and remember.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_20_1.png)

The Tip icon indicates things that you can do to make your job easier.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_20_2.png)

The Warning icon highlights potential pitfalls. With this icon, I’m telling you: “Watch out! This could hurt your system!”

![](img/b7e91b81e0d84c8a5261ee14a48991b2_20_3.png)

The Technical Stuff icon marks technical information that could be of interest to an advanced user (or those of us aspiring to be advanced users).
