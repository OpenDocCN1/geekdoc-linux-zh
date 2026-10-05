
[content]
# Linux all over

The Linux operating system has been ported from the 32-bit Intel architecture to a series of other architectures, including Alpha, STRONGARM, and SPARC, giving users a choice of machine manufacturer and keeping the Linux kernel flexible for new processors. The Linux operating system now handles multiprocessing (more than one CPU or mathematical and logical programming unit per system box). In addition, projects are in the works to provide sophisticated processing capabilities, such as:

- High availability, that is, having the computer run reliably all the time
- Scalability, that is, adding more computer power by adding system boxes rather than faster CPUs

This last feature—known as Beowulf clusters—is enabling organizations to create machines of supercomputer capabilities at a fraction of the price of supercomputers. In certain cases, Extreme Linux systems have been made from obsolete PCs, costing the organizations that make them nothing in material costs.

- Real-time processing, typically to control machinery or test equipment

# Using Linux in Different Ways

Linux is a versatile operating system. Initially the sole domain of computer science students, Linux is now used by businesses and governments to cut costs and improve performance. You can use Linux in a variety of ways: as a desktop workstation; as a server system; as the basis of an embedded system (such as a smart VCR or a robot); or even as a supercomputer. Another major use of Linux is Internet service providers (ISPs), who use it to provide information and services to the Internet and the World Web. And thanks to the thousands of people working on different parts of Linux, the system becomes more flexible and capable with each passing day.

# Personal workstation

With the powerful Linux operating system, you can run many programs at the same time, handle the needs of more than one user at a time, and use high-quality graphics. Linux can handle files and programs of immense size. When used with the 64-bit Digital Alpha processor, for example, Linux can handle data terabytes (thousands of billions of characters) in size. Linux has a sophisticated window system called X Window System (also known as X Windows, XI, or simply X) and can share files not only with most UNIX systems but also with Microsoft Windows, OS/2, and other operating systems.

![](img/96a9ce6a13d8d15ed05f867f41574278_40_0.png)

# 14 Part I: Introducing Linux

Linux also includes the following:

- Web browsers
- TCP/IP
- Compilers
- Freeware programs (such as mail readers, image editors, circuit design programs, and text formatters)

> TIP
> And if the number of freeware programs ported to Linux doesn't satisfy you, commercial applications such as databases, data manipulation programs, and office suites have been ported to Linux, too. With Linux, you can have the same environment on your notebook computer, desktop workstation, and large server system.

# File and print server

Because of its multitasking capability, virtual memory, and powerful file system, Linux works as well as a file and print server for Microsoft Windows systems. A software product SAMBA allows all PCs to communicate with the file system and printers attached to a Linux machine. AppleTalk allows the same file and printer sharing for Apple computers. And, of course, Linux can share files and printers with UNIX systems. By using Linux to do this work, you can save a lot of money because the operating system and the layered software that provide these services are freely available.

# Internet/intranet service provider

Many capabilities of the Internet (outside a single business) and intranets (internal to a single business) are possible because of HTML and the World Wide Web. UNIX systems were at the forefront of these developments, Linux shares many benefits of that heritage. Both the Internet and intranets require similar services:

- Firewalls to keep the bad guys out
- FTP so that the good guys can get files and software
- Telnet so that people can log in and use your machine remotely
- Web servers so that people can see your Web pages
- NFS to share files over the network

Many ISPs use Linux to deliver these services to customers not only because Linux is free but also because the source code for the entire operating system is available. When a problem arises, ISPs can correct it quickly rather than wait for a commercial software vendor to correct the problem.

How critical is a timely correction? Well, in 1997, a problem with TCP/IP result from a deliberate misuse of a program called ping affected almost every UNIX system in the world. This problem would allow bad guys to shut down other people's UNIX systems. The world needed a fix — and quickly! A fix for Linux was on the Internet four hours after the problem was identified, and people could get the fix easily and apply it to their systems. Various commercial UNIX vendors took weeks to develop the fix and send it to their customers.

# Three-tier client/server

Whoa! What the heck is three-tier client/server? It simply means that most computer problems can be broken down into three separate problems, or tiers:

- Data storage and retrieval
- Data manipulation
- Data presentation

When you break a problem down into these three levels, the problem is typically easier to solve and easier to change later as necessary. Until recently, the data presentation level consisted of Microsoft systems running on the desktop (perhaps using Visual Basic to develop the interface). The data manipulation level and the data storage and retrieval level consisted of UNIX or older systems communicating over the network.

Now, however, the data presentation level can be a Linux system running a freely distributed Web browser or a freely distributed Java system (a portable environment for applications). By using Linux, some firms can save thousands of dollars on operating system costs yet still receive required security and operating system robustness.

Like most UNIX systems, Linux also has sophisticated tools that make it a good second-tier system. Linux can extract data from several types of databases or reports kept in older systems, and then sort, combine, and otherwise manipulate the data, passing the newly results to the presentation level on the desktop.

Finally, Linux has the facilities to act as a good storage and retrieval level. Several commercial database packages work with Linux. If you can't afford a commercial database package, you can use one of the freely ones, such as Postgres.

The three-tier concept is to divide work logically, but after you accomplish that, you can put all three pieces of functionality on one computer.

# Turnkey system

A turnkey system is put together once and then duplicated in hundreds or thousands of places. Typical turnkey systems are information kiosks, hotel reservation systems, doctor and lawyer office systems, and automotive diagnostic systems. Linux is perfect for this work because it provides the security, protection, and stability that turnkey systems need without requiring payments for many copies of the operating system. For example, one application that we know was needed on 4,000 systems. If the business had to pay, say, $500 for the operating system, the project would have cost $2 million extra, just to pay for the operating system.

# Chapter 2

# Accessorizing Linux

- In This Chapter
- About SuSE Linux
- Getting Linux for free — or not
- Using Linux ala MS-DOS or Windows
- Examining text editors
- Making the most of mail interfaces
- Marveling at multimedia programs
- Cavorting with commercial products

The SuSE Linux For Dummies CD-ROM is a fully functional version of SuSE Linux, which is a great distribution. Although there are a few distributions of Linux to choose from, this book focuses on SuSE Linux. Every distribution of Linux, at the core, uses the same operating system. In that sense they are all the same. So, what is the difference? Each distribution is different in certain ways, such as the manner in which you install and manage them. To familiarize you with Linux in general, we show you some text editors and mail interfaces, and demonstrate a few other programs, just to whet your appetite. (In other chapters, you see these programs in greater detail.)

## About SuSE Linux

Linus Torvalds and the Linux development team created the Linux operating system kernel. The kernel includes the software for managing memory, files, programs that are running, networking, and various hardware devices. Think of the kernel as a cop directing traffic.
