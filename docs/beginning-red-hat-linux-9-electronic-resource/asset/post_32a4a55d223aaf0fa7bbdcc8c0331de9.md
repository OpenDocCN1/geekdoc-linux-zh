
## Introduction

Of course, this phenomenon, and its potential, has been noticed in the commercial sector, and now Linux has a healthy complement of commercial vendors achieving the seemingly impossible – doing business by selling a product that is essentially free! Of course, in order to do this, these organizations (which include SuSe, Debian, Mandrake, Red Hat, and so on) have been required to innovate and add value to the basic Linux package. The various distributions, packages, and add-ons created by these organizations have matured alongside the basic Linux operating system itself.

The latest Red Hat Linux release – version 9 – is a perfect example of this innovation. While it’s available for free download, Red Hat also sells the package in a variety of forms. For home users there’s a boxed set of CDs containing the Linux operating system, a huge assortment of open source productivity software, Red Hat’s patented Bluecurve interface, and a Demo subscription to Red Hat Network – the vendor’s support, updating, and information network. For corporate users the deal is much the same, but with the emphasis placed more firmly upon support.

Finally, through the combined efforts of both individual developer communities and distribution vendors, there are now Linux versions available that can compete on a level playing field with proprietary software such as Microsoft Windows. This means that Linux is a serious contender both on your home PC and in large-scale production situations.

## Why Choose Linux?

Why might you choose Linux for your operating system, rather than one of its competitors? Here are a few points you might like to consider:

- **Size and speed:** A basic Linux installation can consume as little as 475MB of hard disk space and will run quite happily on as little as 64MB of RAM. Compare this to Unix (which often requires more than 500MB) or Microsoft Windows 2000 (which recommends a minimum 2GB hard disk and 128MB RAM). The difference is due to the efficiency of the Linux operating system and (most of) the applications that run on it.

- **Security:** One significant reason for Linux’s excellent reputation as a secure environment is that its source code is completely accessible, and continues to be viewed by many pairs of eyes. Linux’s open source standpoint means that people *other than the vendor* can check for incomplete or tampered source code. The more people that study Linux’s source code, the more bugs (and security flaws) can be spotted. Of course, that’s only half the story – the other half is that the infrastructure is in place for easy bug-reporting, discussion, and bug-fixing. The result of all this is that *more of the bugs* get spotted *more quickly*, and they’re fixed faster.

In addition to the numerous security applications (such as firewalls) available, many Linux distributions are *specifically* created with a view to providing a highly secure environment. Examples include the Immunix OS (http://www.immunix.com – a commercially available hardened Linux) and Bastille Linux (http://www.bastille-linux.org – a hardening script that can be run on your Linux machine after installation).

- **Standards and support:** Linux's compliance with both Unix standards allows it to interoperate with a number of different operating systems and file systems. Linux can talk to Netware, Macintosh, and Windows networks with ease.

- **GNU software support:** There is a wide variety of software freely available through the GNU project – including development software, office applications, system administration tools, and so on. The OpenOffice suite of applications is one such example and is covered in more detail in Chapter 5. You'll come across others over the course of this book, and we survey a selection of open source applications in Chapter 13.

- **GUI support:** If you like to communicate with your operating system through a nice graphical user interface (GUI) with windows, panels, and menus, then Linux will satisfy you. Whether you're using the GUI to increase productivity or just for fun, you can choose from a number of GUIs, including Bluecurve, KDE, and GNOME.

Moreover, Linux does not force you to use the operating system GUI, and for those who are prepared to explore the command line interface (CLI) the benefits include greater flexibility and lower overheads. It's for this reason that many server administrators in serious production environments eschew the GUI in favor of better flexibility and performance.

- **Cost:** Linux is freely available – what more can you say?! And if you're a business customer, the healthy vendor competition makes for very reasonable support contract prices.

## What Is Red Hat Linux 9?

As we've already mentioned, a number of organizations have created distributions of Linux. Typically, a Linux distribution includes a specific version of the Linux kernel, a collection of components and applications, an installation program (the type of thing more commonly associated with the Windows platform), and often some kind of support arrangement.

One of the most popular distributions comes from Red Hat Inc. – indeed, depending on which of the independent studies market reports you read, Red Hat currently holds more than 50% of the Linux vendor market.

Red Hat Linux comes in a variety of different versions, including:

- Personal Edition (currently at version 9)
- Professional Edition (currently at version 9)
- Advanced Server (currently at version 2.1)
- Itanium (64-bit processor – currently at version 7.2)

Each version contains features appropriate to certain scenarios; these are:

- Small office or home
- Small or medium business
- Enterprise or corporate applications

The following matrix demonstrates which versions are suited to which scenarios:

| | Home | Small Business | Medium Business | Large Business | Enterprise | Other |
|---|---|---|---|---|---|---|
| Personal | √ | √ | | | | |
| Professional | √ | √ | √ | | | |
| Advanced Server | | | √ | √ | √ | |
| Itanium | | | | | | √ |

NOTE: For simplicity, the Enterprise entry in the table is a consolidation of different versions available from Red Hat; these are branded as AS, ES, & WS. For more information on these, take a look at http://www.redhat.com/software/rhel/.

You’ll notice that we’ve used ticks to indicate where a version is suitable for a particular scenario, but we haven’t placed any crosses in the table. This is quite deliberate: if you’re the kind of power user who has a home network and wishes to use some of the advanced features offered only by the Advanced Server edition, then why not? The beauty of Linux is that it’s open and doesn’t demand anywhere near the hardware requirements expected of other operating systems.

So that old machine you had hidden under your desk, destined for the rubbish heap, may be of use after all – dig it out, install Red Hat Linux 9, and use it as a web server or printer server!

## What Is Covered in This Book?

Each chapter in this book builds upon the knowledge developed in earlier chapters, so that there’s a natural path through the book from beginning to end. As you gain confidence and begin to explore Linux further, you’ll also find that this arrangement of topics should help you use the book as a reference.

Here’s a brief description of the chapters in this book:

- Chapter 1 takes you through the process of installing the operating system. It explains how to prepare for the installation, so that you don't get any nasty surprises halfway through. It also explains each step of the installation process, so you know what it's doing, and helps you to get exactly what you want from the installation.

- Chapter 2 introduces the basics of Linux. This chapter takes a tour of the desktop interface, so you can see exactly how to start using Linux. It also explains some fundamental topics that will help you to get the most out of your Linux machine - user accounts, the Linux file system, hardware configuration, and managing your machine's resources.

- Chapter 3 discusses how to configure your Linux machine to connect to the Internet, or to a local area network, so that you can start to send and receive e-mails and use the Internet.

- Chapter 4 introduces the concept of packages. In order to use the components and applications that are supported by Red Hat Linux, we must first install the packages that contain them. This chapter will explain how to go about installing new packages, upgrading packages, and removing any packages that you don't need. There are also many applications out there that are not available in package form, so we'll also have a look at another common format - tarballs.

- In Chapter 5 we'll start to explore the many applications that we can use on Linux to perform our everyday tasks - things like web browsers, office applications, and MP3 players. This chapter introduces just a small proportion of the bewildering array of applications that come with Red Hat Linux 9, and explains where you can find more!

- Chapter 6 tackles the notion of the shell. In fact, you will have been using the shell already in the first five chapters of the book, to type commands and execute them, so that Linux can run them and respond accordingly. Now we examine the shell more closely, and look at combining commands into a script, defining the input to (and output from) a script, and how to build logical structures into scripts, get them to run in specific circumstances, and manage multiple tasks at the same time.

- Chapter 7 presents a detailed explanation of the Linux file system. We'll talk about how to manage your files and directories, and how to use the shell to generate and manipulate the output from predefined or custom scripts. We'll also talk about how Linux allows you to access the file systems of remote and detachable devices such as networked file systems, floppy disks, CD drives, and handheld devices, using a process known as mounting.

- Chapter 8 takes a closer look at user accounts and user groups, and how to manage them. This includes a discussion of permissions and privileges, and provides just enough on the basics of security to prepare us for Chapter 9.

- Chapter 9 describes how you might configure your Linux machine to provide services to other machines on a network. In particular, we'll examine how to set your machine up as an FTP server, a web server, a file server, a printer server, a mail server, or a DHCP server.
