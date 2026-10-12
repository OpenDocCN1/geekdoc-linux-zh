| Software Package | Description |
|:---|:---|
| RCS | The Revision Control System is used for version control and management of source files in software projects |
| Sed | A stream-oriented version of the `ed` text editor |
| Sharutils | A package that includes `shar` (used to make shell archives out of many files) and `unshar` (to unpack these shell archives) |
| Tar | A tape archiving program that includes multimedium support; the capability to archive sparse files, handle compression and decompression, and create remote archives; and other special features for incremental and full backups |
| Texinfo | A set of utilities that generates printed manuals, plain ASCII text, and online hypertext documentation (called info), and enables users to view and read online Info documents |
| Time | A utility that reports the user, system, and actual time that a process uses |

# GUIs and applications

Face it — typing cryptic Linux commands on a terminal is boring. For average users like us, using the system through a graphical user interface (GUI, pronounced "gooey") that gives us pictures to click and windows (small $u$) to open is much easier. This is where the X Window System, or X, comes to the rescue.

X is kind of like Microsoft Windows, but the underlying details of how X works is completely different from Windows. Unlike Windows, X provides the basic features of displaying windows on-screen, but it does not come with any specific look or feel for graphical applications. That look and feel comes from GUIs, such as GNOME and KDE, which make use of the X Window System.

![](bbox=[0.11, 0.755, 0.2, 0.84])

Until recently XFree86 from the XFree86 Project (www.xfree86.org) was the commonly used X Window System implementation for x86 systems. However, around version 4.4, some changes to the XFree86 licensing terms caused concerns to many Linux and UNIX vendors — they felt that the licensing terms were no longer compatible with the GNU General Public License (GPL). In January 2004, several vendors formed the X.org Foundation (www.x.org) to promote continued development of an open source X Window System and graphical desktop. The first release of X.Org X11 uses the same code as that used by XFree86 4.4, up until the time when the XFree86 license changes precipitated the creation of X.Org Foundation.