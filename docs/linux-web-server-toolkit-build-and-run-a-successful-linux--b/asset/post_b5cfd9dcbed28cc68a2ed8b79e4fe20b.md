
# Linux Web Server Toolkit

Sales figures for Linux are not available in precise form because the companies that sell Linux are all privately held and because many users purchase multiple updates in a single year, making accurate statistics harder to gather. However, the latest information seems to indicate that more than 10,000 copies of Linux are being purchased each month worldwide. That figure is in addition to the tens of thousands that are distributed in books and magazines and downloaded from FTP sites.

# Applications for Linux

The number of applications available for Linux has jumped tremendously in the past 18 months. The Linux Commercial HOWTO and the partner-related information on the Caldera Web site are two good places to track the progress of commercial application development for Linux. Several URLs are listed in Table 2-1.

# Table 2-1 Sites Tracking Lists of Available Linux Applications

| Site | URL |
|---|---|
| Linux Applications and Utility Page | http://www.chariott.com/linapps.html |
| Linux Commercial HOWTO | http://www.caldera.com/LDP/HOWTO/Commercial-HOWTO.html (or at other LDP sites) |
| Caldera OpenSolutions Catalog | http://www.caldera.com/ |
| Scientific Applications for Linux | http://SAL.kachinatech.com |

The past 18 months have seen applications added from the top vendors in the U.S. and Germany in categories such as databases, office suites, vertical applications such as POS and accounting, developer tools, and even games. Figure 2-3 shows a page of Caldera's online catalog of applications.

The availability of Wabi, a SunSoft product allows Linux to run on 16-bit Windows applications, opens a new area for the use of Linux as a desktop or home-computing system. But that's another story.

The number of anecdotal stories about Linux has been climbing in the Internet newsgroups and the press. In lieu of the statistics that are still hard to gather (but keep watching; I expect the analysts IDC and Gartner will catch on (soon), stories like the following, which I witnessed, fuel the enthusiasm of all Linux believers.

# Chapter 2: Using Linux for Your Web Server

![](img/e01f1106dd2902613fa07890c8baa7e6_68_0.png)

Figure 2-3: A page from Caldera's OpenSolutions catalog of Linux applications.

A Linux company representative wanted to talk with the biggest mail-order warehouse in Great Britain, without expecting much success. While waiting in the lobby, a technical support person recognized the package and expressed his support for Linux. So then the marketing and executive people got talking, and someone suggested they needed a technical person to help talk over the value of these Linux products. In the Linux supporter. The conversation progressed, and the Linux company rep. suggested that the mail-house Web server might run on Linux. "No way," came the response, until a sheepish technician confirmed "Yes, the whole system has been running on Linux for months." Now they sell Linux.

When you consider all of Linux's features and benefits, it goes without saying we can expect to see it taking hold more and more. Organizations are beginning to see the value in Linux, and the dangers that once held them back from using it are being assaged by validation from informed technical people and commercial Linux providers.

# Summary

This chapter summarized the benefits of Linux as a Web server. It also provided some background information on Linux, including the interesting history of its creator, the loyalty of its stalwart advocates, and why its licensing and means of distribution make this product a little different from similar yet commercial products.

In this chapter you've learned the following:

- Linux is GPL, which means, as long as you follow the GPL terms, and you can make redistribute it as long as you follow the GPL terms, and you can make changes or upgrades to it as long as you distribute or make them available.

- A Linux distribution is a collection of software that includes the Linux kernel, collections of utilities, a graphical system, and numerous other components.

- The key benefits of Linux include: low cost, high performance, stability, an impressive amount of available, powerful Web tools–including Web servers, firewalls, hardware support, HTML conversion and validation tools, statistical tools, and other handy dooddads– and finally, Internet integration.

In Chapter 3, you'll learn how to select the specific software that you'll need to set up a Web server. This chapter covers not only the Linux operating system, which I'll discuss at length, but the Web server program and accompanying tools. Chapter 4 focuses on the Linux system and the Web server.

# Chapter 3

# Choosing Your Software

NOW THAT YOU'RE MORE familiar with Linux system and how to plan your Web server, this chapter discusses choosing a Linux system and the Web server software that you will install and use to run your Web site. Of course, the CD-ROM in the back of this book includes all the software you need to install and run a complete Web server. But as different people have different needs, you may want to add or alter the software in favor of other options. This chapter's key topics include the following:

- How to choose the Linux distribution that's right for you
- Top Linux providers and what they offer
- Evaluating your technical requirements
- The differences between Web server software products, and how to choose the best one for you

# Choosing a Linux Distribution

Before you can install your Web server, you need to have an operating system already chosen to run it. Because you purchased this book, I assume you've either already chosen Linux or are leaning heavily towards it. But as Chapter 2 pointed out, Linux is not so much a product as it is a technology. This may seem like a moot point, because the CD-ROM in the back of this book contains a complete Linux distribution, from start to finish, with everything you need to install a new operating system and get a complete Web server running on. However, as many users have almost religious feelings about the Linux distribution they choose to run on their systems, it seems to present a few options.

Considering that all Linux distributions are basically packaged Internet downloads consisting of a kernel and some utilities, you wonder why different Linux systems exist. The differences between distribution types are really not that big, but because we're talking about your operating system, they have far-reaching effects.

The UNIX operating system became fragmented over time because different companies licensed it and creating different versions. That meant an application that ran on an SGI UNIX machine would not run on an IBM RS/6000 machine. These machines were based on different microprocessor chips, but even UNIX systems running on Intel-based PCs have separate versions: one for SCO UNIX, one for Solaris, and so forth—despite the fact that the applications are probably 98 percent identical and in many cases can be recompiled from one system to the other in a matter of days. Unfortunately, the same sort of thing is starting to happen in the Linux world. Different distribution makers have arranged things in the way they think best. But applications that work on one Linux system may not work perfectly on another Linux system. The problem is not so serious because most applications that Linux currently run source code. So if the application doesn't run, check the options file, recompile the application, move the libraries, and it will usually run.

Other, commercial Linux distributions do not have that luxury. The result is that commercial software companies must do one of the following:

- Support an undetermined number of Linux versions with unknown differences (because the user has unlimited ability to alter the system)
- Develop for a single, specific version of Linux.

Most software developers who want to enter the Linux market seem to be taking the second route. As a result, you see AppWare for Red Hat Linux or AppGen for OpenLinux. These applications may run on other Linux systems, but they are developed with a single Linux as a reference platform, and that is usually the only platform on which they are supported by the manufacter.

# The Basic Differences Between Distributions

The differences between Linux distributions are most noticeable in the areas:

- Installation
- Filesystem standard
- Initialization scripts
- Included software packages
- Philosophy
