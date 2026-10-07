
## CHAPTER 25 Office Productivity Applications

![](img/446debe023486a07fde575245cf7a3ff_871_0.png)

FIGURE 25.17 The KDE Dictionary, found under the Accessories menu, can also be conveniently called from a KDE panel applet.

Under the Extras menu, there are a multitude of useful applications, including these:

- * The AddressBook application
- The Kandy application, which syncs your address book to your cell phone
- KArm, an alarm clock application, and KTimer, a stopwatch app
- KNote, a yellow "sticky note", and Kijots, a small, organized note-taking utility that is useful for jotting down notes when you are reading a book or listening to a lecture
- The GnuCash personal money manager
- The KTouch touch-typing tutor
- The KVocTrain vocabulary builder application

The Extras menu also includes other programming environments, graphics viewers, and dozens of other applications, including games. You should take some time to search through the Extras menu and experiment with some of the productivity (and nonproductivity) tools you find there.

## A Look at an Open-Source Office

Mark Davis, the director of Information Systems at Lake Taylor Transitional Care Hospital (LTH) in Norfolk, Virginia (http://www.laketlor.org), has recently transitioned the facility from use of SCO UNIX to Linux.

Because LTH uses a thin-client topology and all applications are served from a center located throughout the facility, special attention to network bandwidth issues was necessary. Although it was recognized that commercial applications would be used when no open-source alternative was available, applications that emphasized nonproprietary, open standards were given the highest consideration. Using open-source applications allowed Davis to edit the source code and customize the applications for use at LTH. Nonproprietary, open standards permitted the easy integration of applications into the overall system.

A common modification was to remove functionality that represented security compromises (such as access to command prompts or unneeded functions) and to reduce network bandwidth (such as removing animated icons and splash screens).

With the new Linux system in place, the LTH staff enters a work that presents all the productivity applications that are necessary in a modern business. The total cost of ownership (TCO) is significantly reduced, and the system is as stable or more stable than when LTH used commercial SW UNIX.

Among others, the open-source applications at LTH are Mozilla, Dillo, HylaFax, OpenOffice, Seynon, Seypled-clayed, IceWM, the GIMP, Apache, Postfix, Gnumeric, J-Pilot, Quanta, Webal, dclit, and vnc. LTH uses a number of commercial applications, including Retail, Netscape, Word, FoxBase, Merge, Application, Gerimenu, Context Codelink, Monette Ultrracare, Kronos Time Keep Center, and AIS Xess. Because one single computer running Microsoft Windows (modified to limit security problems) is now used with VNC to run the application. (See Chapter 27, "Using Emulators and Other Cross-Platform Tools in Red Hot Linux") to learn more about VNC.

## Productivity Applications Written for Microsoft Windows

Microsoft Windows is fundamentally different from Linux, yet you can install and run some Microsoft Windows applications in Linux by using a Red Hat-supplied application named Wine. Wine enables you to use Microsoft Windows and DOS programs on UNIX-based systems. Wine includes a program loader that can execute a Windows binary, along with a .dll library that implements Windows command calls, using the equivalent UNIX and X11 command calls. To learn more about Wine and other tools that are available for working with Microsoft Windows applications in Red Hot Linux, see Chapter 27.

To see if your favorite application is supported by Wine, you can look at the Wine application database, at http://appdb.winehq.org/appbrowse.php.

## CHAPTER 25 Office Productivity Applications

## Relevant Red Hat Linux Commands

The following commands give you access to productivity applications, tools, and processes in Red Hat Linux:

- fax—A script that acts as a front end to the Efax application
- gimp—a graphical image editor for X
- koshell—KDE’s KOffice office suite shell
- kspread—KDE’s KSpread spreadsheet
- oword—The word processor in OpenOffice
- gnumeric—a spreadsheet editor for GNOME
- mrproject—a project management client for GNOME
- abiword—a graphical word processor for GNOME
- pilot—xfer—a comprehensive command-line tool for PalmOS data users

## References

- http://www.openoffice.org—The home page for the OpenOffice.org suite.
- http://www.pclinusonline.com/modules.php?name=News&file=article&sid=3199—A set of links to tips, tricks, and enhancements for OpenOffice.org. One link at the site is to PDF file that explains how to use OpenOffice.org as a database front for MySQL.
- http://www.gnome.org/gnome-office/—The GNOME Office site.
- http://www.koffice.org—The KOffice site.
- http://en.hancom.com/—The Hancom Office site.
- http://www.sun.com/software/staroffice/6.0/—The StarOffice 6.0 site.
- ftp://http.corel.com/pub/linux/Office2000/updates/installscript/**—A download for an installed script that enables an error-prone installation of Corel’s Word Office 2000 suite under Red Hat Linux and other distributions. Alternatively, you can try http://linux.corel.com/products/wpo2000_linux/index.html.
- http://bulldog.tzo.org/webcal/webcal.html—The home page of the excellent WebCal Web-based calendar and scheduling program.
- http://www.horde.org/projects.php—The Horde Project homepage.
- http://quanta.sourceforge.org—The Quantum Plus Web development tool for KDE.
- http://www.kronos.com/discover/prod_serv/tkc.htm—A Linux-based time-keeping system that supports open standards and is more affordable for the competition.
- http://www.hamrick.com/vsm.html—The VueScan commercial scanning application, which supports a wider range of scanners that the SANE software.

## CHAPTER 26

## Multimedia Applications

## IN THIS CHAPTER

- Burning CDs in Red Hat Linux
- Sound and Music
- Viewing TV and Video
- Using Still Cameras with Red Hat Linux
- Using Scanners in Red Hat Linux
- Graphics Manipulation
- Reference

This chapter provides an overview of some of multimedia, including audio and video. With the new Linux system in place, you'll see how to create and manipulate graphics.

## Burning CDs in Red Hat Linux

Burning (or creating) your own CDs is a fundamental skill for Linux enthusiasts. The CD (and so DVD) has become the standard medium for multimedia content due to the increasing larger of media files. (Individual songs, even in compressed audio, usually require several megabytes of storage space.) You can use CDs to:

- Record and store media data, as backup files, graphic images, and music
- Rip audio tracks from a music CD (ripping refers to extracting music tracks from your own CD and compile your own CD for your personal use
