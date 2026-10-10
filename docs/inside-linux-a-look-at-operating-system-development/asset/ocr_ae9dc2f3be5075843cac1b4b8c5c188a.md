# 1.4. TEMPORARY SHORTCOMINGS

DEC Alpha$^{23}$, MIPS$^{24}$, PowerPC$^{25}$, and SPARC$^{26}$.

Other efforts are in progress, but have not yet provided results.

# 1.4.2 Linux Doesn't Run MS-DOS Programs

Although Linux does not offer a complete virtual machine system, there is a package called **dosemu** which emulates enough of the x86 hardware that MS-DOS can be run inside a Linux process. The package is designed so that neither MS-DOS nor all its applications programs can tell they are not running on the base hardware.

At the time of this writing, **dosemu** has provided a sufficiently complete emulation to boot Microsoft Windows 3.1.

Sections 4.3.2 and 5.2.5 discuss the operation of a virtual machine.

# 1.4.3 Linux Doesn't Do Windows

Microsoft Windows is another operating system for Intel x86 hardware. (Actually, it’s an extension to MS-DOS, but we won’t quibble.) Programs written for this system cannot be directly executed on a Linux system. The WINE$^{27}$ project will overcome this limitation. The Wine FAQ (Frequently Asked Questions and answers) says Wine stands for “**W**indows Emulator, or **W**ine Is Not an Emulator. Both are right. Use whichever one you like best.” Wine provides a program loader and execution environment that includes an emulation library. All the system calls are converted to the appropriate Linux/X Window System calls.

The current condition of this project is “90% done, with the other 10% expected to take another 90% of the time.” Many third party programs run under Wine, but it appears that programs from Microsoft exploit undocumented or ill-documented calls to the system. Once these calls are understood, support for them can be added.

The X Window System is a powerful graphical user interface included in all Linux distributions.

+   23 http://www.a2star.net.com/\~axplinux
+   24 http://www.fnct.fr/linux-mips
+   25 http://liber.stanford.edu/linuxppc
+   26 http://www.geog.ubc.ca/sparclinux.html
+   27 http://www.princeton.com/\~pdg/wine-faq.html