
112 Chapter 5 • History of Linux

## Red Hat Linux

When Linux was first made available, setting up a working Linux system was quite a chore. However, Linux fans soon created Linux distributions, suites of software that made it relatively easy to install, configure, and use Linux. Two of the most popular early distributions were Soft Landing Systems (SLS) and Slack; Slack is still available today.

Red Hat, Inc. was founded in 1994 by Bob Young and Marc Ewing. Soon thereafter, in 1995, Red Hat, Inc. created a Linux distribution called Red Hat Linux. Unlike other distributions at that time, Red Hat was a package-based distribution, meaning that component programs were contained in package files that also contained information describing the programs. A utility program called the Red Hat Package Manager (RPM) was used to install packages. Because it maintained a database of installed, RPM made it simple to update a Linux system, a crucial capability in view of the rapid rate of Linux software. Today, almost every Linux distribution is package-based; the majority of Linux distributions use RPM as their package manager.

Red Hat Linux is the dominant Linux distribution. It has won Inf awards for three consecutive years, an unprecedented achievement. Red Hat, Inc., the company founded by Young and Ewing, is now a widely trusted corporation with a capitalized value in the billions. In addition to Red Hat Linux, the company offers services such as telephone support, on-site consulting, developer training, certification programs, and priority access updates.

## Linux Resources

Linux improves daily, so keeping up with Linux requires having—and access to information that's updated daily. This section lists some Web sites and newsgroups that will help you stay current with the Linux scene.

### Linux Information

- Groups of Linux Users Everywhere (GLUE), www.linuxjournal.com/glue
- Linux Documentation Project, metalab.unc.edu/LDP
- Linux HOWTOs, howto.tucows.com
- Linux International, www.li.org

Copyright©2000 SYTEX, Inc., Alameda, CA www.sysex.com

- Linux Knowledge Base, linuxukb.cheek.com
- Linux OnLine, www.linux.org
- Linux Start, www.linuxstart.com
- Linux.com, www.linux.com
- Red Hat, Inc., www.redhat.com

## Major Linux Distributors

- Caldera Systems, Inc., www.caldera.com
- Corel, www.corellinux.com
- Debian GNU-Linux, www.debian.org
- Linux Mandrake, www.mandrake.com
- Red Hat, Inc., www.redhat.com
- Slackware, www.cdrom.com
- Storm Linux, www.stormlinux.com
- SuSE, www.suse.com
- TurboLinux, www.turbinolux.com

## Other Linux Vendors

- ASL, Inc., www.aslab.com
- Cheap Bytes, www.cheapabytes.com
- Infomagic, www.infomagic.com
- Linux Central, www.linuxcentral.com
- Linux General Store, www.linuxgeneralstore.com
- Linux Mall, www.linuxmall.com
- Linux System Labs, www.l1sl.com
- LinuxCare, www.linuxcare.com
- VA Linux Systems, www.valinux.com

## Linux News

- FileWatcher, filewatcher.org
- Freshmeat, www.freshmeat.net
- Kernel Traffic, kt.linuxcare.com
- Linux Gazette, www.ssc.com/lgg
- Linux Information HQ, www.linuxhq.com
- Linux Journal, www.linuxjournal.com
- Linux Kernel, www.kernel.org
- Linux Magazine, www.linux-mag.com
- Linux Radio Show, www.thelinuxshowhow.com
- Linux Today, www.linxtoday.com/index.html
- Linux Weekly News, www.lwn.net
- Linux World, www.linuxworld.com
- Linux-2000 Online, www.linux-2000.org
- Slashdot, www.slashdot.org

## Linux Newsgroups

- comp.os.linux.announce (moderated)
- comp.os.linux.answers
- comp.os.linux.hardware
- comp.os.linux.misc
- comp.os.linux.setup
- comp.os.linux.x

## Summary

In this chapter, you learned about the history of Linux, the GNU project, and Open Source Software. You also learned about the features of Red Hat Linux and where to go to get more information about Linux. The most important topics covered are:

- Unix Linux is based on concepts originally implemented by Dennis Ritchie and Ken Thompson of AT&T in their Unix operating system.
- GNU and FSF Richard Stallman founded the FSF and the GNU Project to ensure software freedom. The goal of the GNU project was to create a free, Unix-like operating system.
- GPL The GNU General Public License is a form of copyright that protects software freedoms, including the rights to use, modify, and distribute software.
- Linux Linux is a Unix-like operating system distributed under terms of the GPL. Linux includes a kernel originally created by Linus Torvalds and utilities and programs originally created by the GNU Project.
- Red Hat Linux Red Hat, Inc. distributes Red Hat Linux, the leading distribution.

## Key Terms

Before going to the next chapter, be sure you're familiar with the following terms:

- copyleft
- development kernel
- FSF (Free Software Foundation)
- GNU
- GPL (General Public License)
- kernel
- Linux distributions
- OSS (Open Source Software)
- stable kernel

## Review Questions

1. Which of the following is an operating system ancestor of Linux?
A. C
B. GNU
C. Solaris
D. Unix

2. Which of the following was the principal author of the Linux kernel?
A. Dennis Ritchie
B. Andrew Tannenbaum
C. Ken Thompson
D. Linus Torvalds

3. Which of the following was the founder of the Free Software Foundation and the GNU project?
A. Marc Ewing
B. Richard Stallman
C. Linus Torvalds
D. Bob Young

4. Which of the following version numbers would denote a stable Linux kernel?
A. 1.1
B. 1.2
C. 2.1
D. 2.2

5. Which of the following characteristics made Red Hat Linux superior to other Linux distributions?
A. Cost
B. Efficiency
C. Maintainability
D. Scalability

6. Linux was originally implemented for what type of computer?
A. Intel 286
B. Intel 386/486
C. Intel Pentium
D. Motorola 68000

## Answers to Review Questions

1. D. C and GNU are not operating systems, although GNU is intended to someday be one. Solaris is not an ancestor of Linux.

2. D. Linus Torvalds, a Finnish computer science student, wrote the original Linux kernel.

3. B. Richard Stallman, a former MIT researcher, founded the FSF and the GNU project.

4. B, D. The decimal part of the version number is even for a stable kernel and odd for a development kernel.

5. C. Packages made Red Hat Linux more maintainable than other Linux distributions, because it was simpler to update the system.

6. B. Linus Torvalds implemented Linux for the Intel 386/486.

## Installation

## PART

## Chapter 6

### Installation Planning

RHCE PREPARATION TOPICS COVERED IN THIS CHAPTER:

- Understand the importance of determining system needs.
- Know what information may be required during installation.
- Know how to select the installation user interface.
- Know how to select the installation class and type.
- Know how to design a partition structure.
- Know how to use fips to split an MS-DOS partition.
- Know how to select and prepare installation media.
- Know how to select installation media.
- Know how to select components and packages.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_144_0.png)

Planning is an important part of realizing an effective and efficient execution, no less so in system administration than in other endeavors. This chapter describes the tasks you should perform and the decisions you should make before installing Red Hat Linux. If you follow the instructions in this chapter, you can expect the installation of Red Hat Linux to go smoothly, with only an occasional exception.

### Determining Needs

The first step in installation planning is to determine the needs that the system must satisfy. For example, a worker who will use the system as a workstation for preparing graphics will have a different set of needs than a system administrator who plans to use the system primarily as an FTP server. Once you know what the system must do, you're ready to decide what hardware is needed and how Red Hat Linux should be installed and configured.

### Gathering Information

Installation will go more smoothly if you've collected information about the hardware on the target system. If you have the flexibility to choose the hardware, choose hardware that's listed in the Red Hat Hardware Compatibility List (HCL) over other hardware. Be wary of devices, such as CD-ROM drives, that have proprietary interfaces. Also be wary of WinModems and WinPrinters.
