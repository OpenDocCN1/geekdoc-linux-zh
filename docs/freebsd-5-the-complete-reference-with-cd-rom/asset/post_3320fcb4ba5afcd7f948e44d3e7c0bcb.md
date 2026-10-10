
## Chapter 1: FreeBSD Requirements

Some UNIX variants are known as a *microkernel*. This approach uses a smaller kernel that communicates with separate nonkernel components that handle more traditional kernel tasks, such as accessing filesystems. Microkernels tend to be more rigidly structured. Both monolithic and microkernel designs have their proponents.

FreeBSD is an open source OS. Specifically, most FreeBSD components use what's generally known as the *BSD license* (<http://www.opensource.org/licenses/bsd-1-license.html>). This license allows modification and redistribution under whatever terms the person doing the redistribution desires. Thus, in theory, somebody could take FreeBSD, modify it, and sell the result under a proprietary commercial license, or under another open source license. Another popular open source license is the *GNU General Public License* (GPL), which requires that modifications be distributed under the GPL. The Linux kernel uses the GPL, and this difference in licensing drives some of the philosophical differences between FreeBSD and Linux proponents. (To be sure, not everybody has strong opinions on this matter of *license terms*.) As a general rule, FreeBSD favors using software components that use the BSD license, and Linux distributions tend to rely more upon packages that use the GPL. Although these licenses don't directly affect the feel of their OSes, many utilities are available in alternate forms that use different licenses; thus, FreeBSD feels different than Linux because the two use a somewhat different mix of utilities.

Some UNIX-like OSs use proprietary (non-open-source) licenses. For instance, Sun's Solaris and IBM's AIX are commercial UNIXes. Sometimes you can use such an OS for free or for a low cost, as in the free Solaris for x86. Other times, you must pay for a commercial UNIX license. Just as there are tensions in the open source world between proponents of the GPL and BSD licenses, there are tensions between open source and commercial software proponents. These are philosophical and economic differences, though; FreeBSD works much like its commercial UNIX cousins.

# Note

> *Commercial and open source software need not be incompatible. You can run open source programs on a commercial OS, or commercial programs on an open OS. Nonetheless, most FreeBSD programs use open source licenses.*

Aside from FreeBSD, some popular UNIX-style OSs are:

- **NetBSD** NetBSD is one of three OSs derived from 386/BSD (as described later in the section “The Development of FreeBSD”), the other two being FreeBSD and OpenBSD. NetBSD differs from FreeBSD, in that NetBSD has been ported to many more CPUs. Its licensing and overall design are very similar to those of FreeBSD, but FreeBSD remains more popular because it's more heavily promoted and is arguably somewhat easier to install and use.

- **OpenBSD** OpenBSD's claim to fame is security. Its developers have gone to great lengths to create an OS that's not easily compromised. Like NetBSD, OpenBSD is quite similar to FreeBSD in configuration, licensing, and available software.

- **Linux** You can think of Linux as a family of open source OSes. Technically, Linux is just the kernel; a Linux *distribution* includes the kernel and the software packages that create a usable OS. FreeBSD differs more from Linux than from NetBSD and OpenBSD in overall configuration style and the details of included tools.

> **Note**
>
> *Some people unfamiliar with the UNIX world think that FreeBSD is a Linux distribution. It’s not. FreeBSD doesn’t use the Linux kernel, nor does it follow common Linux practices, such as the use of SysV startup scripts. FreeBSD is best thought of as an OS derived directly from the Berkeley Standard Distribution (BSD), as described later in the section “The Development of FreeBSD.” Linux is a free reimplementation of UNIX with weaker links to the early BSD and AT&T UNIX.*

- **Solaris** Sun’s Solaris is a commercial UNIX variant that’s most commonly found on Sun’s server hardware. This hardware uses SPARC CPUs, and is often used for heavy-duty servers that compete against high-end x86 systems and above. Solaris is also available to run on x86 computers, and so can be used on some of the same computers that run FreeBSD. Solaris on x86 has a weaker selection of drivers than does FreeBSD, though. If you need to develop programs for Sun computers, running Solaris on an x86 may be desirable; but for most other purposes, a BSD or Linux is probably a better choice for x86 computers. Sun hardware can make a good high-end server computer, though.

- **AIX** IBM’s commercial UNIX variant is known as AIX, and it runs on proprietary IBM hardware. Like Sun systems, AIX computers are aimed at the high-end server market, so their level of competition against FreeBSD is limited.

- **IRIX** Most of SGI’s workstations run a commercial UNIX variant known as IRIX. SGI’s claim to fame in the past has been computers that are optimized for high-end graphics work, such as doing special effects for major motion pictures. Today, less expensive x86 computers are eating into this market, but SGI and IRIX are still powerful forces in this arena.

On the whole, FreeBSD competes most directly against its cousin BSDs and against Linux. FreeBSD is the most popular of the BSDs on x86 hardware, and so has an advantage when it comes to finding support. FreeBSD was developed with an eye for easy installation and administration; NetBSD and OpenBSD are somewhat weaker in these areas. You might want to consider OpenBSD for enhanced security or NetBSD for support on non-x86 CPUs, though. The overall feel of Linux is different from that of any of the BSDs. Linux supports a bit more hardware and commercial software, and the licensing issues are different. If you’re just starting out and want a general-purpose open source UNIX-like OS, chances are either FreeBSD or Linux will work quite well. The Linux world tends to be a bit more chaotic, though, and the differences between distributions can be confusing to new users.

For the most part, FreeBSD doesn’t compete as directly against the commercial UNIX variants, which run on hardware that’s a step or so above typical x86 hardware, especially in floating-point math operations. If you have a need for some high-powered systems along with less expensive computers, a mix of FreeBSD on x86 systems and more powerful servers running Solaris, AIX, or IRIX can make sense. Although they're not identical in configuration, the skills it takes to administer or use a FreeBSD system are similar to those needed on commercial UNIX variants. In some cases, a high-end x86 system can compete directly against low-end Sun, IBM, or SGI hardware. Usually, the x86 system running FreeBSD is less expensive, but it may be harder to find service contracts or the like for FreeBSD.

### The Software Environment

The preceding sections described where FreeBSD fits in the range of OSs available today. This information can help you decide whether to run FreeBSD or some other OS. If you decide to run FreeBSD, though, you must know how it interacts with other OSs. This interaction includes both other computers on a network and other OSs run on the same computer. It’s also helpful to know something about FreeBSD’s history, to better understand its design philosophy and its strengths and weaknesses as an OS. This section covers these issues.

### The Development of FreeBSD

The history of FreeBSD, and of UNIX generally, is complex. It begins with the development of the first (very primitive) version of UNIX in 1969 at AT&T. From that point on, collaborations with the University of California at Berkeley contributed by increasing numbers of volunteers, replacement of existing code, and development of “workaline” utilities have all come into play. The original AT&T UNIX has spawned several variants (also known as forks in the code base). Good ideas developed in one fork have often found their way into other forks, and there have been periods in UNIX history in which UNIX vendors have worked to reduce the differences caused by code forks. Nonetheless, UNIX today is not a single OS, but rather a family of related OSs.

> **Note**
>
> *Technically, the name UNIX applies only to versions of the OS that are officially sanctioned. Some people use UNIX (fully capitalized) to refer to such official versions of the OS, and Unix (with an initial capital only) to refer to workaline systems. Because this is a very subtle distinction, this book uses UNIX to refer to an official UNIX or the family of OSs as a whole, and UNIX-like systems or similar phrasings when it’s important that the reference be interpreted as referring not just to official UNIX but to similar OSs, such as Linux.*

After the original development of UNIX by Ken Thompson and Dennis Ritchie in 1969, the first important milestone in the branch that led to FreeBSD was the delivery of a copy of Version 4 of UNIX to UC Berkeley in 1974. Over the next several years, the faculty, staff, and students at Berkeley became familiar with UNIX, wrote programs for...
