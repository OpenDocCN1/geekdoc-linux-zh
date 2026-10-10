# Chapter 5: Accessing and Running Applications 237

consists of three steps: Installing Win4Lin (available in RPM format), installing the guest operating system (Windows 98, 2000, or ME; XP is still experimental), and setting up a guest session. When you run a full Windows system from a Linux desktop, installing and running any Windows applications you choose.

+   * **QEMU** — QEMU (www.qemu.org) is an open source project that acts as a processor emulator. It can either emulate a full system or work in user mode emulation (where it can be used to test processes compiled for different CPUs). In full system emulation, QEMU can run a variety of operating systems, including Windows 3.11, 95, 98SE, ME, 2000, and possibly XP.

To try applications intended for other operating systems, QEMU can also run several Linux (Fedora, KNOPIX, Mandrake, Morphix, Debian, and others) and other UNIX-like systems (NetBSD, Solaris, and others). QEMU can take advantage of virtualization features, using KVM, that have recently been added to the Linux kernel (described later in this chapter).

The rest of this section describes how to get and use WINE to run Windows applications in Linux. To get WINE for your Fedora system, you can go to the following places:

+   * **WINE in Fedora** — As of Fedora 7, WINE became part of the main Fedora software repository. The wine and wine-core packages are needed to use WINE. Additional WINE support comes in the following packages: wine-capi (ISDN support), wine-cms (color management), wine-esd (ESD sound support), wine-jack (JACK sound support), wine-ldap (LDAP support), wine-nas (NAS sound support), wine-tools (useful Windows utilities), and wine-twain (scanner support). Add wine-docs for further documentation or wine-devel, for WINE development components.

+   * **Cedega** — A commercial version of WINE called Cedega (formerly called WineX) is available from TransGaming, Inc. (www.transgaming.com). TransGaming focuses on running Windows games in Linux, using WINE as its base. See Chapter 7 for descriptions of Cedega.

+   * **CodeWeavers** — If you need Microsoft Office or Web browser plug-ins, CodeWeavers (www.codeweavers.com) offers CrossOver Linux. Although CrossOver Linux costs some money, it offers friendly interfaces for installing and managing the Windows software. A 30-day free trial is available.

While it’s true that you can run many Windows applications using WINE, some fiddling is still required to get many Windows applications to work. If you are considering moving your desktop systems from Windows to Linux, the current state of WINE provides an opportunity to see if some Windows applications you need might run in Linux.

Besides developing software, the WINE project maintains a database of applications that run under WINE (http://appdb.winehq.org). More than 1000 applications are listed, although many of them are only partially operational. The point is, however, that the list of