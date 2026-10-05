# Chapter 1 Where to Start

community-based development project called Fedora. The split was motivated by a variety of technical, economic, logistic, and legal reasons.

The distributions were initially similar, but Fedora had made some significant changes over the last five years and the two systems aren't currently synchronized in any meaningful way. RHEL offers great support and is effectively impossible to use without paying fees to Red Hat.

The CentOS (centos.org) collects source code that Red Hat is obliged to release under various licensing agreements (most notably, GNU Public License) and assembles it into a complete distribution that is eerily similar to Red Hat Enterprise Linux, but free of charge. The distribution lacks Red Hat's branding and a few proprietary tools, but is in respects equivalent. CentOS operates to full binary and bug-for-bug compatibility with RHEL.

OS is an excellent choice for sites that want to deploy a production-oriented distribution without paying tithes to Red Hat. A hybrid approach is also feasible: front-line servers can run Red Hat Enterprise Linux and themselves of Red Hat's excellent support, while desktops run CentOS. This arrangement covers the important bases in risk and support while minimizing cost and administrative complexity.

# Example UNIX distributions

![](bbox=[0.185, 0.503, 0.238, 0.545])

Solaris is a System V with many extensions from the company formerly known as Sun Microsystems now part of Oracle. Sun UNIX (as it was called in the mid-80s) was originally the progeny of Berkeley UNIX, but a (now historic) corporate partnership between Sun and AT&T forced a change of code base. Solaris runs on a variety of hardware platforms, most notably Intel x86 and SPARC.

In Sun's hands, Solaris was free to download and use. Oracle has changed this policy, and current downloads are listed as 90-day free trials. The existence of OpenSolaris, an explicitly free and open version of Solaris, complicates the picture as well. At this point (mid-2010), Oracle's exact plans for Solaris and OpenSolaris remain unclear.

The release of Solaris 11 is expected some this year, and indication is that it will hold closely to OpenSolaris. In this book, the composite system we refer to as "Solaris" is based on production Solaris 10 and OpenSolaris releases with guidance from our network of deep-core spies within Oracle. In a few cases, we note specifics for Solaris 10 or OpenSolaris.

![](bbox=[0.185, 0.814, 0.238, 0.853])

HP-UX is based on Hewlett-Packard hardware platforms. It's closer to the ancestral tree than either Solaris or AIX, but HP has kept pace with developments in the OS world and has added a variety of its own enhancements. Now that HP has begun supporting Linux, the future of HP-UX is less clear.

+   1. See page 1264 for some background on BSD, System V, and the general history of UNIX.