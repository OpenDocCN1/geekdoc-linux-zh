I wrote this chapter in response to several readers of earlier editions of this book who wanted to replace their Windows servers with Linux servers. I hope this chapter will help start them, and you, on the road to taking full advantage of powerful networked Linux features from your easy-to-use Mac desktops.

# Looking Inside Mac OS X

Inside Apple computers for the past few years is an operating system referred to as *Mac OS X*. You might also hear Mac OS X referred to as *Jaguar*, *Panther*, or *Jaguar* (or *Leopard*, which was released in October, 2007). As with Linux, OS X has a free UNIX-like operating system at its core that, in this case, has been turned into a commercial product. That core, instead of being a Linux kernel, was originally based on a BSD-derivative open source project called Darwin (*www.opendarwin.org*).

Although Mac OS X and Linux are very different on the surface, there are many *striking* similarities. If you open a Terminal (shell) window on your Mac, you'll find that you can use many of the same basic commands that you can use from Linux. In addition, many of the same open source projects are included in both operating systems. These include:

+   - Samba (Windows file/printer server)
+   - Apache (Web server)
+   - CUPS (Linux print service)
+   - Sendmail (mail transport agent)
+   - BIND (DNS server)

There are also a few differences:

+   - Fedora is primarily covered under the General Public License, while OS X is based partly on an Open Source license and partly on a proprietary license. In August, 2003, the Apple Public Source License (APSL 2.0) was released (*www.opensource.apple.com/apsl*) and is now certified as a Free Software License from the Free Software Foundation.
+   - Fedora uses the Linux kernel; Mac OS X is based on a Mach micro-kernel surrounded by FreeBSD services. (Apple refers to this kernel as XNU and released it as a component of the Darwin open source operating system.)
+   - Most configuration in Fedora and RHEL is done using system-config windows, which often create text-based configuration files (mostly in the /etc directory) from command-line or GUI applications; Mac OS X stores the configuration file in its own NetInfo database, which is manipulated primarily by GUI tools as well as by the `niutil` command.