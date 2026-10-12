
# X11 Directory Structure and Upgrading

| Path | Description |
| :--- | :--- |
| /usr/X11R6/include/doc | Documentation and release notes |
| /usr/X11R6/lib | X11 software libraries needed by X clients and programmers |
| /usr/X11R6/man | X manual pages |

If you installed and configured X11 when you first installed Red Hat Linux, you’ll find that most of the X Window System resides under the /usr/X11R6 directory (although a number of GNOME and KDE clients will be found under /usr/bin).

If you have an older version of X11 installed, you can use Red Hat’s rpm command to upgrade X. First, you’ll need to remove your existing XFree86 installation. You should first find all your XFree86 package names. You can do this easily by using rpm command’s query option and the fgrep command like this (your output may look different):

```bash
# rpm -qa | fgrep XFree
```

The output typically includes packages such as:
*   XFree86-libs-4.0.1-1
*   XFree86-devel-4.0.1-1
*   XFree86-ISO8859-2-75dpi-fonts-4.0.1-1
*   XFree86-ISO8859-7-75dpi-fonts-1.0-7
*   XFree86-ISO8859-9-75dpi-fonts-2.1,2-13
*   XFree86-75dpi-fonts-4.0.1-1
*   XFree86-tools-4.0.1-1
*   XFree86-xdm-4.0.1-1
*   XFree86-100dpi-fonts-4.0.1-1
*   XFree86-ISO8859-2-1.0-12
*   XFree86-ISO8859-2-Type1-fonts-1.0-12
*   XFree86-ISO8859-7-1.0-7
*   XFree86-ISO8859-7-Type1-fonts-1.0-7
*   XFree86-ISO8859-9-2.1,2-13
*   XFree86-VGA16-3.3,6-33
*   XFree86-doc-4.0.1-1
*   XFree86-xf86-4.0.1-1
*   XFree86-4.0.1-1
*   XFree86-twm-4.0.1-1
*   XFree86-ISO8859-2-100dpi-fonts-1.0-12
*   XFree86-ISO8859-7-100dpi-fonts-1.0-7
*   XFree86-ISO8859-9-100dpi-fonts-2.1,2-13
*   XFree86-cyrillic-fonts-4.0.1-1

You can then erase various packages at a time by using the rpm command and its -e or erase option, along with a wildcard .rpm package name, like this:

```bash
# rpm -e XFree\*ISO\*
```

Next, insert the first Red Hat CD-ROM and make it available on your system using the mount command (it may also be mounted automatically):

```bash
# mount /mnt/cdrom
```

Since Red Hat Linux provides an entry in the filesystem table `/etc/fstab`, you could also mount the CD-ROM under the `/mnt/cdrom` directory by specifying your system's CD-ROM device, `/dev/cdrom` (a symbolic link to your CD-ROM's device), like this:

```bash
# mount /dev/cdrom
```

From the command line, use `rpm` like this:

```bash
# rpm -Uvh /mnt/cdrom/RedHat/RPMS/XFree86*.rpm
```

If you did not install X, you can use Red Hat's `rpm` command to install the software. However, you should know that the process will involve solving many .rpm package dependencies!

### Note

You can also try using the `gnorpm` command to install the software. Select Preferences and then set the interface preference `RPM` path to the `RPMS` directory on your mounted Red Hat CD-ROM. KDE also includes a similar package manager client named `kpackage`.

Depending on the software installed, these directories can take up 40-400MB of hard drive space, and even more if you install a lot of X window managers, programming libraries, or other software. (A typical full installation of XFree86 is about 80-123MB, depending on the number of extra clients.)

## Choosing a Configuration Tool

The largest hurdle most new X users face after installing XFree86 is coming up with a working `XF86Config` file. This file can be initially generated during your install, but if you have a problematic graphics chipset, you may need to "tweak" your configuration after booting, or may even want to postpone configuring X11 until after you first log in. This is sometimes the safest approach; trying to log in to a Linux system configured to boot directly to X11 without a properly configured system can be confounding. Fortunately, if you run into this problem, you can simply press `Ctrl+Alt+Delete`, reboot, then either press `Ctrl+X` at the Red Hat LILO login, or pass the kernel argument `linux single` at the LILO boot prompt like this:

```bash
boot: linux single
```

If you already have a working setup, chances are your old XFree86 3.3.6 `XF86Config` may work, as there is some compatibility built into the new server. However, the new version of XFree86 uses a new layout and structure for the `XF86Config` file!

If you're starting from scratch, one of the first things you should do after installing X and before configuration is to read as much of the documentation as possible. Although the daring and brave will launch right into configuring X11, even experienced users will benefit from reading about the latest XFree86 developments and checking the XFree86 documentation for tips about their specific hardware.

Documentation at the time of this writing was still a bit sparse, but you will find information under the /usr/X11R6/lib/X11/doc directory. Table 4.1 contains the details of this directory for XFree86 4.0.1. Note that documentation for the release is still somewhat sparse; just because you don't see a README file for your graphics chipset does not mean that it is not supported! This is true for Cirrus Logic, NeoMagic, Tseng, and Trident chipsets. You'll find detailed information regarding protocols, libraries, clients, and other services under the /usr/share/doc/XFree86-doc-4.0.1 directory.

### Table 4.1 XFree86 Documentation

| File | Description |
| :--- | :--- |
| DESIGN | Extensive server design information |
| LICENSE | Licensing and copyright statement |
| README | General information about the current XFree86 release |
| README.Deciga | Information for DEC 21030 users |
| README.DGA | How to program for the XFree86 DGA interface |
| README.DRI | Information about DRI support |
| README.DRIcomp | Compilation information about DRI |
| README.S3 | Notes for S3 chipset users |
| README.s3virge | Notes for S3 VIRGE, ViRGE/DX, ViRGE/GX, ViRGE/MX, and ViRGE/VX users |
| README.SIS | Notes for SiS chipset users |
| README.apm | Notes about the Alliance Promotion chipset |
| README.ati | Information about XFree86's ATI Adapters video drivers |
| README.chips | Notes about Chips and Technologies chipsets |
| README.cyrix | Info for Cyrix MeidaGX users |
| README.fonts | Using fonts with XFree86 |
| README.i740 | Info for Intel 740-based graphics cards |
| README.i810 | Info regarding Intel 810 motherboards |
| README.mouse | Details about XFree86's X11 mouse support |
| README.r128 | ATI Rage 128 information |
| README.rendition | Details about Rendition chipset users |
| RELNOTES | The definitive release notes for XFree86 |
| ServersOnly | How your directories should look when building XFree86 X servers |
| Status | Driver status in the release |
| videoBoardD8 | Info on the PC98 XFree86 server |

If you're new to X11, first read the man pages for X and XFree86 for an overview of X. Before you begin configuring X, you need to know some technical details about your computer and your computer's video card and monitor. Here is some of the information that will help:

- The type, make, name, or model of video card installed in your computer
- How much video RAM (not system RAM) is installed for your card
- The type of clockchip used by your video card chipset
- The type of mouse you use (PS/2, serial, or USB, for example)
- The type, make, name, or model of monitor attached to your computer
- The vertical and horizontal refresh rates for your monitor (such as 55~100 vertical, 30~60 horizontal)
- The type of keyboard you use

Armed with this information, you then have to choose the method or tool for configuring XFree86 and generate a correct XF86Config file for your system. There are a number of ways to do this:

- XFree86 The main X11 server's built-in configuration facility
- Xconfigurator Red Hat's graphical X11 setup tool
- xf86config XFree86's traditional text-only tool
- xf86cfg XFree86's graphical configuration client
- Manual Create your own XF86Config with a favorite text editor

All these methods may be done from your console's command line or from a terminal window's command line.

Xconfigurator and xf86cfg have the advantage of providing a graphical interface; xf86config asks a series of questions in a text-mode screen; and XFree86 performs the configuration automatically. If you're lucky, your computer's hardware will exactly
