
## Linux doesn't have the software I need.

It depends on what type of software you need. If you're looking for a custom application to run a specific type of business (inventory management for veterinarians who specialize in parrots), yeah, you're probably going to be out of luck.

But if you're looking for generic desktop-type applications, you may find this to be less true than you think. There are open-source equivalents to virtually all popular Windows applications, and most of them come packaged with the top Linux distributions.

## Linux won't run my Windows software.

Okay, so you've got a piece of software that runs only on Windows, and it's not getting ported to Linux in the foreseeable future. Perhaps it's a vertical-market application that is tied tightly into the Windows API. Or perhaps it's a horizontal application but one that doesn't have a Linux equivalent.

Fear not. There are a couple of ways to run Windows software on a computer that has Linux installed on it. The first is an open-source software application called WINE (or its commercial equivalent, Crossover Office), and the second is a tool called VMware that runs Windows and Windows applications natively.

WINE is a program installed on a Linux computer. After it's installed, a Windows program is installed "on top of it." The Windows program runs on top of WINE. WINE translates all of the Windows operating system calls into the equivalent Linux operating system calls. As a result, the Windows program never knows it's running on a Linux computer. WINE can be tricky to install and configure, though. Crossover Office is a wrapper for WINE; it handles all of the installation and configuration issues, and works virtually flawlessly. And Transgaming's version of WINE, WINE X, lets you run a bunch of the most popular Windows games under Linux.

VMware is a piece of software that emulates a second computer, completely through software. After installing VMware, you can install a second operating system within VMware. Then, while running that second OS, you install applications that are native to that OS, just as if it were the only OS on the computer. While somewhat resource intensive, VMware provides a mechanism for you to run Windows applications perfectly on a Linux machine.

## You have to use the command line.

The command line is the Linux equivalent to what Windows power users think of as a "Command Box" or a "DOS Box." For those of you who grew up with MS-DOS, the command line isn't as intimidating as for those who grew up with a GUI. In either case, while the command line can be useful at times, it is rarely needed anymore for day-to-day use.

## You have to compile everything.

In the early days of Linux, most software came packaged simply as source code, which meant in order to use it, you had to compile it first to create an executable binary (the program itself), and then install the binary itself.

Realizing that more and more users wanted to simply use the software without a lot of fuss, software developers began taking advantage of the installation features provided by various distributions. Red Hat's RPM, SuSE's YUM, and Debian's apt-get mechanisms make installing a new software package as easy as double-clicking on a file or running a command or two at the "command line."

You can still find distributions that require you to roll up your sleeves, pull out the first can of a 12-pack of Jolt from the cooler, and compile every package. Gentoo, for example, does this as part of the installation, and the result is a Linux installation that is tuned precisely for your specific hardware.

## You don't have to worry about security.

Everyone "knows" that Linux is more secure than Windows, and as a result, many users just ignore security on their Linux box. Bad idea.

It's true that virus writers primarily target Windows boxes. However, Linux boxes are not invincible; they can be taken over by a trojan engine or crippled by an adroitly written exploit.

Some of the newer distributions are also set up poorly, with the regular user account having root (think "administrator") access, and it's possible for you to install a bunch of programs and services that you don't need or want, and thus provide potential vulnerabilities.

Bottom line: You still need to keep your operating system patched, and it's a good idea to run a virus scanner.

## I can't use my existing hardware.

Nonsense. Current Linux distributions are as accepting of most hardware as current Windows versions. There is always a chance that you've got an off-brand printer/scanner/fax machine/dishwasher, or the driver for your specialized second sound card has a bug in it. But generally, you can expect recent releases of Linux to recognize a wide range of hardware right out of the box, and they usually provide options to configure the oddball hardware elements during installation.

## There isn't any technical support.

Again, nonsense. There are several avenues for technical support, and many people would argue that these avenues are better than those provided for proprietary software, because open-source communities aren't under the same type of profit pressure as their for-hire peers.

First of all, paid support is available for distributions that come packaged in a box, such as Red Hat Enterprise, SuSE, and Mandrake. Community-supported distributions like Fedora Core and Debian do not have paid support per se, so read on.

All distributions have online communities that provide a variety of mechanisms for support. First are the mailing lists and forums directly associated with the distribution. Along with mailing lists are the archives—a huge resource for searching for answers, because it's often likely that someone else has had the same question, and has already posted it and received the answer. A third avenue is the set of FAQs (Frequently Asked Questions) provided by most sites.

In addition, hosts of Web sites provide information about using various distributions; a little time spent with one of the major search engines on the Internet (such as Google) often produces worthwhile results.

## It doesn't cost anything.

Well, sort of. There are two sides to this question.

Yes, you can download a copy of Fedora Core, install it, and use it for free. You aren't required to fork out cash if you don't want to. You can download patches, search for other free software, and generally have a grand time without ever shelling out a nickel. If you're going to use it at home, or at work for casual use, you can very likely get away with this route forever.

But if you're going to use Linux for serious work, you might want to consider the cost of your time as well. You can buy a boxed set, and buy a service contract that provides technical support, patches and updates, and perhaps other resources. It's up to you.

## Which Linux?

Linux is a moving target, in large part because of the fact that there are many competitors in the market. Microsoft Windows is manufactured and controlled by one company, and thus there aren't any choices. You get what they want you to have, and no further discussion is allowed. Linux, on the other hand, is different. You have many choices. These choices are called “distributions,” and to understand your choices, you need to understand distributions.

## About Linux “distributions”

Linux is an operating system that was initially created as a hobby by a young student, Linus Torvalds, at the University of Helsinki in Finland. Linux had an interest in Minix, a small version of UNIX, and decided to develop a system that exceeded the Minix standards. He began his work in 1991 when he released version 0.01, and worked steadily until 1994 when version 1.0 of the Linux Kernel was released. Version 2.4 was released in January of 2001, and version 2.6 is showing up in new releases of distributions during the spring of 2004.

Linux, strictly speaking, refers to just the operating-system kernel. This kernel handles what an operating system is supposed to, acting as the traffic cop between the various hardware devices in a computer. It natively supports multi-tasking, as well as multi-user and server capabilities. However, when people talk about “Linux,” they often refer to more than just the kernel, including ancillary components such as GUIs, utilities, installation routines, and other components.

While the term “Linux” is copyrighted by Torvalds, the Linux software was created under the GNU General Public License. As a result, its source code is freely available to everyone who wants a copy. (The GPL does impose a restriction—that modifications to the source code must be returned to the community and made available under the same license.) Because the source code is freely available, anyone can package the source code together with whatever else they desire—applications such as OpenOffice.org or KOffice, utilities such as the Mozilla browser and The GIMP graphical editing tool, and literally thousands more software applications of all kinds and sorts.

These collections are called “distributions,” and more than 200 different distributions are available—some for popular, mainstream use, such as Red Hat, SuSE, and Mandrake; others for hardcore users, such as Debian and Gentoo, and still others that are more specialized.

This, however, doesn't mean that Linux and its assorted distributions are free—companies and developers may charge money for it as long as the source code remains available. Some distributions are free for download, and support is available at a price, while other distributions are produced by consortiums of volunteers, and support is available only online.

Linux may be used for a wide variety of purposes including embedded systems (think Playstation, watches, and machine tools), networking (file and print servers, e-mail servers, Web servers), software development, and as an end-user platform. Each distribution is constantly trying to improve, make itself more user-friendly and easier to install, recognize a larger set of hardware, and so on.

As a result, selecting a distribution for this book was a significant challenge.
