# Chapter 1 • What is UNIX?

essence of the open source software movement. The FSF's GNU General Public License (GPL) parallels this description. Software covered by the GPL

+   - may be distributed and used free of charge.
- in turn be distributed by others for a fee, provided that those who do so do not restrict further distribution and use.
- can be modified to create new versions of the software, but these new versions are also covered by the GPL.
- is copyrighted to the developers of the software and is not in the public domain.
- either must have the source code in a distribution or have it available for down-load.

Linux is covered by the GPL, so it can be considered open source software. Also, because it was not derived from any licensed source code and is not registered with The Open Group, cannot in the strictest sense be accurately designated as a UNIX system. Rather, it is a UNIX clone, meaning that it looks and smells like UNIX, but it really just “mimics the form and function of a UNIX system.” (See “What about All Those Flavors?” at The Open Group’s Web site at www.opengroup.org.)

# 1.4 The Elements of UNIX

So, we now know, more or less, the origins of UNIX. As you can see, there is no such thing as the UNIX operating system. For convenience, I use one form of UNIX for this book, namely HP-UX version 11. HP-UX is based on the System V Release 4 operating system and includes important features from the Fourth Berkeley Software Distribution. Most HP-UX commands are the same as most UNIX implementations. However, you may have to consult the man pages for your particular system.

All UNIX implementations share some general characteristics, and what follows is a brief description of these characteristics. If you are mostly a DOS/Windows person, you should read through this section before looking at later chapters.

# 1.4.1 The Kernel

Every UNIX system has a file, loaded into memory upon system startup, called the kernel. HP-UX calls this file /stand/unix; Red Hat calls it /boot/mlinux. In one sense, the kernel can be considered the operating system itself, since it talks directly to the hardware, handles processes, interrupts, and the like. However, most people think of an operating system as being more than just the kernel; it also includes utilities, compilers, libraries, and editors. So, in another sense, the kernel can be thought of as the memory-resident portion of the operating system.

But there is no doubt that the kernel controls the interaction between user programs and the hardware. You, as a user, do not access the kernel directly. Instead, you run a command or