# Yes, There Are Others

Just when you think all the distributions have been made, another one pops up. These distributions all have their own focuses, each one being created to fill a perceived gap.

For instance, there is Stampede that is optimized from top to bottom to run on Pentium-based systems. There are also distributions targeted at non-Intel platforms such as Yellow Dog for PPC, distributions targeted specifically at Microsoft Windows users such as DragonLinux, and distributions targeted for inexperienced users such as easyLinux.

For a comprehensive list of Linux distributions, including over 120 different distributions, see the Linux Weekly News Distributions page at www.lwn.net.

# The Linux Standard Base Project (LSB)

One of the biggest complaints that software vendors have about Linux is that it appears to be a “moving target.” If you wanted to do so, you could update your systems to the latest version of the C library, the latest alpha-grade kernel, or the latest beta test versions of software on a weekly (sometimes even daily) basis. Some people actually do this, and it is those people who, innocently enough, have given Linux this moving target stigma.

> > There is absolutely nothing wrong with updating a Linux system in this manner. An explanation of how Linux got this image was warranted, however.

This can be fun for a hobbyist or a casual tinkerer, but business users and developers tend to shy away from systems that change weekly. This fear tends to bleed over into the corporate IT world—the same world that has to use the software that developers are trying to keep working under Linux.

For instance, say a developer ported a software package to one Linux distribution that uses the latest version of the GNU C Library (glibc 2.1). The application might work great on that Linux distribution, but when moved to another distribution that uses an older C library (glibc 2.0, or the very old libc version 5), some essential pieces of the library are missing that might prevent the software from running. This implies that a whole slice of Linux users will probably not purchase that software package, or will ring up significant hours of technical support trying to get the software vendor to help with installation.

All in all, it is not a situation in which many vendors want to find themselves. It is situations like this that can prevent a company from porting their software to Linux.

To address this concern, a group was assembled under the umbrella of the Linux Standard Base project to discuss how to develop a solid, stable platform with known, established binaries and libraries with which software developers can reliably port their software. This group is not centered around any particular Linux distribution—far from it, actually. There is representation from at least seven of the top Linux distributions (Slackware being a major exception), some Linux hardware vendors, and volunteers who are driven by the idea of slowing down the moving target syndrome described earlier.