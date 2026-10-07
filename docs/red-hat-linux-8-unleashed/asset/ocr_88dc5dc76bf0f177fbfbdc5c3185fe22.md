# A Look at an Open-Source Office

Mark Davis, the director of Information Systems at Lake Taylor Transitional Care Hospital (LTH) in Norfolk, Virginia (http://www.laketlor.org), has recently transitioned the facility from use of SCO UNIX to Linux.

Because LTH uses a thin-client topology and all applications are served from a center located throughout the facility, special attention to network bandwidth issues was necessary. Although it was recognized that commercial applications would be used when no open-source alternative was available, applications that emphasized nonproprietary, open standards were given the highest consideration. Using open-source applications allowed Davis to edit the source code and customize the applications for use at LTH. Nonproprietary, open standards permitted the easy integration of applications into the overall system.

A common modification was to remove functionality that represented security compromises (such as access to command prompts or unneeded functions) and to reduce network bandwidth (such as removing animated icons and splash screens).

With the new Linux system in place, the LTH staff enters a work that presents all the productivity applications that are necessary in a modern business. The total cost of ownership (TCO) is significantly reduced, and the system is as stable or more stable than when LTH used commercial SW UNIX.

Among others, the open-source applications at LTH are Mozilla, Dillo, HylaFax, OpenOffice, Seynon, Seypled-clayed, IceWM, the GIMP, Apache, Postfix, Gnumeric, J-Pilot, Quanta, Webal, dclit, and vnc. LTH uses a number of commercial applications, including Retail, Netscape, Word, FoxBase, Merge, Application, Gerimenu, Context Codelink, Monette Ultrracare, Kronos Time Keep Center, and AIS Xess. Because one single computer running Microsoft Windows (modified to limit security problems) is now used with VNC to run the application. (See Chapter 27, "Using Emulators and Other Cross-Platform Tools in Red Hot Linux") to learn more about VNC.

# Productivity Applications Written for Microsoft Windows

Microsoft Windows is fundamentally different from Linux, yet you can install and run some Microsoft Windows applications in Linux by using a Red Hat-supplied application named Wine. Wine enables you to use Microsoft Windows and DOS programs on UNIX-based systems. Wine includes a program loader that can execute a Windows binary, along with a .dll library that implements Windows command calls, using the equivalent UNIX and X11 command calls. To learn more about Wine and other tools that are available for working with Microsoft Windows applications in Red Hot Linux, see Chapter 27.

To see if your favorite application is supported by Wine, you can look at the Wine application database, at http://appdb.winehq.org/appbrowse.php.