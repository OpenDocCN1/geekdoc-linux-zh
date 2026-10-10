
## Using DOSBox

To run your classic DOS applications, Fedora includes the dosbox package. To install dosbox, type the following as root user:

```
# yum install dosbox
```

With DOSBox installed, just type **dosbox** to open a DOSBox window on your desktop. From that window, you have an environment when you can run many classic DOS applications. Assuming you have some DOS applications you want to run already stored on your Fedora system, you can make those applications available by mounting the directory containing them. For example, to mount the `/home/chris` directory to drive C in DOSBox, type the following:

```
Z:> mount c /home/chris
```

At this point, you can use standard DOS commands to access and run applications from the directory you just mounted. For example, type **dir c:** to see the contents of the directory you just mounted. Type **c:** to go to that directory. Then just run the DOS applications stored in that directory by typing its name.

To mount a CD-ROM, you need to indicate the file system type when you mount it. For example:

```
Z:> mount d /media/disk -t cdr
```

For information on using special keys and features in dosbox, refer to the dosbox README file (`/usr/share/doc/dosbox-*/README`).

## Running Microsoft Windows applications in Linux

There are several promising approaches you can take to get your Windows applications to work during a running Linux session. Here are a few of them:

- **WINE** — The WINE project (www.winehq.org) has been making great strides in getting applications that were created for Microsoft Windows to run in Linux and other operating systems. WINE is not really an emulator because it doesn't emulate the entire Windows operating system. Instead, because it implements Win32 application programming interfaces (APIs) and Windows 3.x interfaces, the WINE project is more of a “Windows compatibility layer.” WINE doesn't require that Windows be installed. It can, however, take advantage of Windows dll files if you have some to add.

- **Win4Lin** — Win4Lin (www.win4lin.com) is a commercial product for running a Windows system in Linux. You can try the software free for 14 days. Installation consists of three steps: Installing Win4Lin (available in RPM format), installing the guest operating system (Windows 98, 2000, or ME; XP is still experimental), and setting up a guest session. When you run a full Windows system from a Linux desktop, installing and running any Windows applications you choose.

- **QEMU** — QEMU (www.qemu.org) is an open source project that acts as a processor emulator. It can either emulate a full system or work in user mode emulation (where it can be used to test processes compiled for different CPUs). In full system emulation, QEMU can run a variety of operating systems, including Windows 3.11, 95, 98SE, ME, 2000, and possibly XP.

To try applications intended for other operating systems, QEMU can also run several Linux (Fedora, KNOPIX, Mandrake, Morphix, Debian, and others) and other UNIX-like systems (NetBSD, Solaris, and others). QEMU can take advantage of virtualization features, using KVM, that have recently been added to the Linux kernel (described later in this chapter).

The rest of this section describes how to get and use WINE to run Windows applications in Linux. To get WINE for your Fedora system, you can go to the following places:

- **WINE in Fedora** — As of Fedora 7, WINE became part of the main Fedora software repository. The wine and wine-core packages are needed to use WINE. Additional WINE support comes in the following packages: wine-capi (ISDN support), wine-cms (color management), wine-esd (ESD sound support), wine-jack (JACK sound support), wine-ldap (LDAP support), wine-nas (NAS sound support), wine-tools (useful Windows utilities), and wine-twain (scanner support). Add wine-docs for further documentation or wine-devel, for WINE development components.

- **Cedega** — A commercial version of WINE called Cedega (formerly called WineX) is available from TransGaming, Inc. (www.transgaming.com). TransGaming focuses on running Windows games in Linux, using WINE as its base. See Chapter 7 for descriptions of Cedega.

- **CodeWeavers** — If you need Microsoft Office or Web browser plug-ins, CodeWeavers (www.codeweavers.com) offers CrossOver Linux. Although CrossOver Linux costs some money, it offers friendly interfaces for installing and managing the Windows software. A 30-day free trial is available.

While it’s true that you can run many Windows applications using WINE, some fiddling is still required to get many Windows applications to work. If you are considering moving your desktop systems from Windows to Linux, the current state of WINE provides an opportunity to see if some Windows applications you need might run in Linux.

Besides developing software, the WINE project maintains a database of applications that run under WINE (http://appdb.winehq.org). More than 1000 applications are listed, although many of them are only partially operational. The point is, however, that the list of applications is growing, and special attention is being paid to getting important Windows 2000 and XP applications running.

Although not an open source product, Win4Lin is another good way to run Windows applications, along with a Linux system on the same running computer. With the open source QEMU project you can simultaneously run Microsoft Windows and Linux operating systems on the same PC. (See http://qemu.org/ossupport.html for a complete list of supported operating systems.)

In general, Windows applications are less likely to break in QEMU than they are in WINE (since you actually run the whole Windows operating system), but performance may not be as good (since you run an operating system within an operating system). The next section describes how to set up Linux to run Microsoft Windows applications using WINE.

## Running Windows Applications in WINE

For WINE to let you run Microsoft Windows applications, it needs to have an environment set up that looks like a Microsoft Windows system. The following section takes you through the steps of installing and configuring the wine RPM available from Fedora. You can install wine over the Internet by typing the following:

```
# yum install wine wine-tools wine-core wine-docs
```

Although you only need the wine and wine-core packages, wine-tools offers some nice graphical tools for working with your WINE environment and wine-docs offers some useful documents in the `/usr/share/doc/wine-docs*` directory for developing software and using WINE. The `yum` command line shown above will also pull in other wine packages from the Fedora repository (such as those that include additional support for sound, scanners, and other features mentioned earlier).

The location of the basic Microsoft Windows operating-system directories for WINE is the `$HOME/.wine/drive_c` directory for each user, which looks like the C: drive to Wine. The `$HOME/.wine` directory is created automatically in your home directory the first time you run Wine Configuration (select Applications → Other → Wine → Wine Configuration) or type the `winecfg` command.

```
$ winecfg
```

This opens the Wine configuration window, where you can do most of your activities to add applications, configure the operating system, and integrate with the desktop. Figure 5-5 shows an example of the Wine configuration window.

![](img/fb202c163797a743c3c6cf236316bc96_272_0.png)

Figure 5-5: Set up your Windows applications in Linux from the Wine configuration window.

### Assigning drive letters

Before you begin installing Windows applications in WINE, you should become familiar with your WINE environment. Drive letters are assigned in the `$HOME/.wine/dosdevices` directory. Select the Drives tab on the Wine configuration window to see which drive letters are assigned. At least drive C: and drive Z: should be set.

To configure additional drive letters, you can select Add (to add an individual drive) or select Autodetect (to have WINE assign all your partitions to drive letters) in the Windows configuration window.

Within the `$HOME/.wine/drive_c` directory (that is, your C: drive), you should see some things that are familiar to you if you are coming from an older Windows environment: `Program Files` and `windows` directories.
