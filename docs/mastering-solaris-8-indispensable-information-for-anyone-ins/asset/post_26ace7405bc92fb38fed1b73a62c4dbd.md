
# Tape Drives

Sun Solaris supports many different tape drives, as was noted earlier in this chapter. Although backing up to tape does not offer immediate restoration of a system whose disk has failed (mirrored disk is a better solution for that), tape does offer the most economical means at the moment to provide an historical record of your disk’s conditions. Many Solaris workstations and servers come with tape drives as standard devices. The following list includes the most common tape media you are likely to encounter:

- 1/2-inch reel tape with a capacity of 140MB
- QIC 1/4-inch tape cartridges with a capacity of 2.5GB
- DDS3 4mm cartridge tape with a storage range of 12GB, DDS2 with a 2GB or 4GB capacity
- Elliptical tape systems with capacities in the 50GB to 75GB range (such as EcRIX and OnStream drives)
- DLT 4000 and 7000 cartridge tape with storage capacities of 20GB and 35GB to 70GB, respectively, from Quantum and other OEMs.
- Linear Tape Open or LTO drives with capacities in the 50GB and greater range

Tape technology continues to advance in capacity and decrease in cost, although not quite as fast as disk, but there is still at least an order of magnitude less cost involved in committing data to tape. Given the rapidly increasing size of hard drives, there is a tendency to use tape systems with greater and greater capacity. Note also that the ranges of storage capacity represent the “native” capacity of the tape versus the capacity you achieve when you commit compressed data to tape. The compression ratio is typically in the range of 2 or 3 to 1, but it can vary considerably based on the data types you store to disk.

## Remote MagTape Protocol

If you remember back to the discussion of addressing earlier in this chapter, tape drives have the device name `/dev/rmt/Xabn`, where X is the drive number, a is the optional density (l = low, m = medium, h = high, u = ultra, and o = compressed), b is the Berkeley (SunOS 4.x) compatibility, and n is the optional parameter of rewind (no letter for no rewind and n = rewind). The initials rmt are taken from the name Remote MagTape protocol. You don’t have to enter optional parameters like density, but if you don’t, the tape drive writes data at its default density, which is typically its highest density.

![](img/256e02a6afce528d264a8d911fa0ff20_241_0.png)

**NOTE** Chapter 12 describes the use of Solaris utilities and third-party applications for working with tape drives, hard drives, and Zip and Jaz drives.

A tape drive may be running on your system as you do other work, or you may want to check the status of a backup on a backup server. In any case, use the Manage Tape (mt) command to display information about your tape drive. The syntax for this command is `mt -f /dev/rmt/X status`. The mt command has a retention parameter and a rewind parameter that let you specify those operations. Many tape drive manufacturers include tape utilities and graphical user interface programs for managing their tapes, such as Veritas Netbackup, Legato Networker, CA ARCServe, and so forth. If your tape drive doesn’t come with one of these programs, you can purchase them, and each program supports a very wide range of devices. Contact the tape drive manufacturer or visit the manufacturer’s Web site to obtain information about programs that support their hardware.

## Summary

Solaris supports devices that can be used to store data, connect to the network, or perform other important kinds of I/O. Devices are addressed as physical devices, and their characteristics are stored in physical device files. Every device has a logical device name.

Devices can access data as block, character, or raw data. Devices require device drivers to provide I/O capabilities to talk to the system kernel. When you install or remove devices and drivers, you need to perform a reconfiguration reboot.

You can partition hard drives to provide flexibility and security to your stored data. In this chapter, you learned about the configuration and contents of the standard partitions or slices that Solaris installs.

Solaris supports a very wide range of peripheral devices, including diskettes, hard drives, CD-ROM drives, tape drives, Zip and Jaz drives, and serial port devices such as terminals that can be controlled from within the operating system. These systems and their support were described in this chapter. Tape drives, which are common peripheral devices that allow you to save an historical record of your system’s data, were also discussed.

# CHAPTER 7

# The Solaris Desktop

**FEATURING:**

- Solaris and GUIs ........................ 224
- The CDE Desktop ........................ 226
- The Front Panel ........................ 253
- Actions ........................ 267
- Customizing the Desktop ........................ 272
- OpenLook Desktop ........................ 280
- The X Window System ........................ 283

![](img/256e02a6afce528d264a8d911fa0ff20_243_0.png)

In this chapter, one of the central chapters in the book, you will learn about the standard graphical interfaces used on Sun Solaris. It isn't always necessary to run a graphical desktop on a Sun workstation or, in particular, a Sun server, but for situations in which a user is interacting with applications, a desktop environment is most often used. Solaris users tend to use the Common Desktop Environment (CDE) as a standard, so this chapter describes this window manager in detail. However, Solaris is capable of running other graphical interfaces, as well as X Windows and X-terminal sessions. All of these other interfaces are briefly described in this chapter as well.

## Solaris and GUIs

Until the mid-1990s, every version of Unix, including Solaris, came with a proprietary windowed graphical user interface, or GUI. There were window standards such as Motif, but they were implemented somewhat differently on each Unix version. Those differences caused developers and users considerable problems and limited the applicability of many programs to one flavor of Unix or another.

The Common Open Software Environment (COSE) led to the development of the Common Desktop Environment (CDE), which is currently the standard of choice for a GUI on many popular forms of Unix. The popularity of Linux as a desktop environment is leading Solaris to use GNOME in the future as CDE's replacement.

You select the Solaris GUI when you log in and select the Common Desktop Environment (CDE) option or the OpenWindows Desktop option from the Session submenu on the Options menu of the Login screen. Most of the windows you will see in this book are based on the CDE because OpenWindows support in Solaris will be phased out sometime in the future. A short section on OpenLook and the OpenWindows desktop is included toward the end of this chapter. Other choices on the Options menu provide for a command-line login.

Efforts to create a GUI as an alternative to the Unix command line began almost at the same time that GUIs were becoming popular in desktop systems (based on the work that had been done at Xerox PARC in the mid and late '70s). By 1984, with the appearance of the Macintosh and soon thereafter with the introduction of the Commodore Amiga, window managers began to be written for various flavors of Unix in many places. The X Windows product (described in more detail in the last few sections of the book) gave rise to an industry interface standard that is in widespread use today. There have been many window managers written for X Windows, some of which are described in the next section. Solaris's two window managers, CDE and OpenWindows, run on X Windows sessions.

Early work on Unix GUIs included systems like the Tab Window Manager (twm), also called Tom's Window Manager, a small and fast window system that ran on X Windows.
