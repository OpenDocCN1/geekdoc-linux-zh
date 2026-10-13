
Recently, Mandrake has diverged more from Red Hat, pushing toward more cutting-edge packages and a faster time to market.

## SLS

The first Linux distribution was the SLS distribution from Soft Landing Software in Canada. It provided convenient, pre-compiled and ready to run sets of packages that could be installed in any combination. SLS reduced the steps that were previously required to install software on Linux systems—search for the source code, download it, extract it, compile it, and hope it installs and works correctly—and saved so much time and effort that many people had no problem with its $150 price tag.

However, it was still rather unfriendly to install, especially from the standpoint of someone migrating to Linux from a DOS background.

## Slackware

The next major distribution answered many complaints that people had about SLS by simplifying the installation and offering a package management system called pkgtool.

For installation, instead of running a command-line program and passing the names of the package sets to be installed as in SLS, Slackware offered a full-screen, menu-driven interface. It enabled the user to browse the package sets that were available for installation, and went the extra mile by offering users the capability to select or deselect individual packages within those sets.

One of its biggest boosts to the Linux distribution world was the management of installed packages. Using plain tarred and compressed archives (.tgz files), the pkgtool program did a fair job of making the installation and removal of software packages more painless. The main problem that occurred—and still occurs because Slackware hasn’t really changed much in this regard—is that some files from individual packages are inevitably left behind when packages are removed. Without a database to keep track of where all the installed files are (such as those used by Red Hat and OpenLinux’s RPM package manager or Debian’s dpkg), it is impossible to know how to cleanly remove files after they are installed. Regardless, Slackware’s package management system does a good job, considering that it just uses ordinary archive files.

Slackware uses a BSD-style initialization scheme. The benefit of this is a simpler system for loading services at boot time. A drawback is that the user does not have very much control over the services that are being started up. For instance, in SysV initialization you can have a different set of services set to start with different runlevels, not unlike the runlevel menu you sometimes get when a Windows 95 system becomes corrupted (Safe Mode with Networking, Safe Mode without Networking, and so on). You cannot do this with BSD initialization such as the one used by Slackware.

Slackware is favored by many as the most traditional of the Linux distributions. Nostalgia and inertia (keeping what is familiar on one’s system) seem to be doing a good job of keeping this distribution alive, not to mention the fact that it is typically quite current with its software versions and technical fortitude. It provides its user base with consistency and an unflinchingly familiar installation system from version to version.

## Yes, There Are Others

Just when you think all the distributions have been made, another one pops up. These distributions all have their own focuses, each one being created to fill a perceived gap.

For instance, there is Stampede that is optimized from top to bottom to run on Pentium-based systems. There are also distributions targeted at non-Intel platforms such as Yellow Dog for PPC, distributions targeted specifically at Microsoft Windows users such as DragonLinux, and distributions targeted for inexperienced users such as easyLinux.

For a comprehensive list of Linux distributions, including over 120 different distributions, see the Linux Weekly News Distributions page at www.lwn.net.

## The Linux Standard Base Project (LSB)

One of the biggest complaints that software vendors have about Linux is that it appears to be a “moving target.” If you wanted to do so, you could update your systems to the latest version of the C library, the latest alpha-grade kernel, or the latest beta test versions of software on a weekly (sometimes even daily) basis. Some people actually do this, and it is those people who, innocently enough, have given Linux this moving target stigma.

> There is absolutely nothing wrong with updating a Linux system in this manner. An explanation of how Linux got this image was warranted, however.

This can be fun for a hobbyist or a casual tinkerer, but business users and developers tend to shy away from systems that change weekly. This fear tends to bleed over into the corporate IT world—the same world that has to use the software that developers are trying to keep working under Linux.

For instance, say a developer ported a software package to one Linux distribution that uses the latest version of the GNU C Library (glibc 2.1). The application might work great on that Linux distribution, but when moved to another distribution that uses an older C library (glibc 2.0, or the very old libc version 5), some essential pieces of the library are missing that might prevent the software from running. This implies that a whole slice of Linux users will probably not purchase that software package, or will ring up significant hours of technical support trying to get the software vendor to help with installation.

All in all, it is not a situation in which many vendors want to find themselves. It is situations like this that can prevent a company from porting their software to Linux.

To address this concern, a group was assembled under the umbrella of the Linux Standard Base project to discuss how to develop a solid, stable platform with known, established binaries and libraries with which software developers can reliably port their software. This group is not centered around any particular Linux distribution—far from it, actually. There is representation from at least seven of the top Linux distributions (Slackware being a major exception), some Linux hardware vendors, and volunteers who are driven by the idea of slowing down the moving target syndrome described earlier.

The LSB project will address compatibility issues between the various Linux distributions by settling on a common set of binaries, libraries, and directory layouts that have been the source of many cross-distribution problems in the past. Hopefully, in the end, software developed or packaged for one Linux distribution will simply plug into another distribution with a minimum of hassles, if any at all.

Anyone who wants to contribute time to this project is encouraged to participate. There are mailing lists and Web pages that cater to the LSB project and that are open to the general public. Observers are encouraged to lurk (read without posting) on the mailing lists in an effort to keep the signal-to-noise ratio high. For this reason, ideas and concerns need to be submitted to committee members instead of the mailing lists. Everyone is encouraged to follow the discussion and consider becoming an official part of the effort, though. Be sure to check the LSB Web page (www.linuxbase.org) for more information on this project.

## The Linux Professional Institute and Linux Certification

The Linux Professional Institute (LPI) was created by a group of volunteers who perceived the need for an accepted certification process that would recognize and certify the talent and hard work of Linux users everywhere. Since its inception, the effort has taken on a life of its own and has now involved some of the Linux movement’s best and brightest in a fully open process aimed at providing certification for all.

The LPI isn’t the only organization offering Linux certification. Others exist. However, LPI is the only one with an open process for developing certification exams. These exams are being developed by the Linux community for the Linux community. Exams are kept to the absolute minimums as far as number and price, but they strive for the highest quality. For more information about the Linux Professional Institute, see their Web page at www.lpi.org.

## How Does Linux Fit In with Other Networked Environments?

Many people within the Linux community want to establish Linux as a viable alternative to other graphical desktop operating systems. This is a good cause to support. Linux has proven itself as a highly stable end-user operating system, and with graphical interfaces such as the ones provided by the K Desktop Environment and GNOME, which are covered in Chapters 3 and 4, migration from other operating systems is becoming easier and easier. In addition, commercial software companies such as Loki Entertainment Software and Oracle have targeted Linux as the platform on which their bread and butter (games and databases respectively) can be served, and so far their porting efforts have gone over quite well with the Linux community in general.
