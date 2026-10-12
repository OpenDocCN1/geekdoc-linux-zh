
The transition for desktop users from Windows to Linux is becoming easier, with great strides being made by projects such as the WINE project. WINE (described later in this chapter) lets you run many Windows programs directly in Linux. WINE also provides a path for application developers to more simply port their Windows code to run in Linux.

The bottom line is that it will take some effort for most people to discard their Windows operating systems completely. However, if you are committed to making Red Hat Linux your sole application platform, there are several ways to ease that transition. Emulation programs let you run many programs that were created for other operating systems. Conversion programs can help you convert graphics and word processing data files from other formats to those supported by Linux applications.

> CROSS-REFERENCE: See Chapter 6 for information on importing and exporting word processing and graphics files.

If you are running Linux on a PC, chances are that you already paid for a Windows 95, 98, ME, XP, NT, or 2000 operating system. You can either run the different operating systems on different PCs or have Windows and Linux on separate partitions of your hard disk. The latter requires that you reboot each time you want to switch operating systems.

The following section describes applications that run in Red Hat Linux that you can use to replace the Windows applications you are used to.

## Finding Windows-Equivalent Applications in Linux

If you are going to use Red Hat Linux as a desktop computer system, you have to be able to write documents, work with graphics, and crunch numbers. You probably also have other favorite applications, like a music player, Web browser, and e-mail reader.

> NOTE: Using WINE technology, the people at Codeweavers, Inc. offer a CrossOver Office product that lets you install and run Microsoft Office in Linux. See the "Running Windows Applications with WINE" section later in this chapter.

To give you a snapshot of what desktop applications are available, Table 5-1 contains a list of popular Windows applications, equivalent Linux applications, and where you can find the Linux applications. Although many of these applications have not reached the level of sophistication of their Windows counterparts, they can be cost-effective alternatives.

### Table 5-1: Windows-Equivalent Linux Applications

| Windows Applications | Linux Applications | Where to Get Linux Applications | Cost |
|---|---|---|---|
| Microsoft Office (office productivity suite) | OpenOffice (openoffice.org) | Included on Red Hat CDs | Free |
|  | Koffice | Included on Red Hat CDs | Free |
|  | StarOffice | www.sun.com/staroffice | $75.95 |
| Microsoft Word (word processor) | OpenOffice Writer | Included on Red Hat CDs | Free |
|  | abiWord | Included on Red Hat CDs | Free |
|  | kword | Included on Red Hat CDs | Free |
| Microsoft Excel (spreadsheet) | OpenOffice Calc | Included on Red Hat CDs | Free |
|  | gnumeric | Included on Red Hat CDs | Free |
|  | kspread | Included on Red Hat CDs | Free |
| Microsoft Powerpoint (presentation) | OpenOffice Impress | Included On Red Hat CDs | Free |
|  | kpresenter | Included on Red Hat CDs | Free |
| Microsoft Internet Explorer (Web browser) | mozilla | Included on Red Hat Linux CDs | Free |
|  | epiphany | Included on Red Hat Linux CDs | Free |
|  | konqueror | Included on Red Hat Linux CDs | Free |
|  | opera | www.opera.com | Free download |
| Microsoft Outlook (e-mail reader) | evolution | Included on Red Hat CDs | Free |
|  | kmail | Included on Red Hat CDs | Free |
|  | Mozilla Mail | Included on Red Hat CDs | Free |
| Adobe Photoshop (image editor) | The Gimp (gimp) | Included on Red Hat CDs | Free |
| Quicken or Microsoft Money | gnucash | Included on Red Hat CDs | Free |
| AutoCAD (computer-aided design) | LinuxCad | www.linuxcad.com | $89 |

### Obtaining Red Hat Linux Applications

Unfortunately, you won’t be able to walk into the average computer store and find a lot of Linux application programs. The best way to get Linux applications (other than those included with your Red Hat Linux system) is to download them from the Internet. They can also be ordered on CD-ROM from several Linux Web sites.

Software packages that are specifically compiled and packaged for Red Hat Linux distributions are almost always available in RPM format. So when you begin scouring the Internet for Red Hat software (as described later), look for software repositories of RPM packages built specifically for the version of Red Hat Linux or Fedora Core that you are using.

### Investigating your desktop

More and more high-quality desktop applications are being packaged with Red Hat Linux, mostly as part of the GNOME or KDE desktop environments. In other words, to start finding some excellent office applications, games, multimedia players, and communications tools, you don’t have to look any further than the Red Hat menu button on your desktop.

So before you start hunting around the Internet for the software you need, see if you can use something already installed with Red Hat Linux. The chapters that follow this one describe how to use publishing tools, play games, work with multimedia, and communicate over the Internet — all with programs that are either on the CDs that come with this book or are easily attainable. Appendix B contains a list of the software packages that are included with the complete version of Red Hat Linux that is packaged with this book.

> **TIP:** To keep up with fixes to software packages that are part of the Red Hat Linux distribution, Red Hat offers a service for automatically downloading and installing packages. Chapter 10 shows you how to use Red Hat Network and the `update` command to update your Red Hat Linux software.

### Finding applications on the Internet

If you don’t already know the names of applications you want to use, there are a lot of places to look for Linux applications on the Internet. If you do know what you want, your best bet might be to head for a software repository that has packages built specifically for Red Hat Linux and Fedora.

Here are a few Web sites that you can browse for software that runs in Linux:

- **Freshmeat** (www.freshmeat.net) — This site maintains a massive index of Linux software. You can do keyword searches for software projects or browse for software by category.
- **SourceForge** (www.sourceforge.net) — This site hosts thousands of open source software projects. You can download software and documentation from those projects from the SourceForge site.
- **Tucows Linux site** (linux.tucows.com) — Both free and commercial software for Linux is available from the Tucows Linux Web site. This site also features news articles on Linux and a listing of software downloads from the site by category.

When you purchase a commercial application, you usually get the application on CD. Installation is often simplified, and hard copy documentation is provided. Of course, when you download software, you get immediate gratification — when you purchase it, you have to wait for the package to arrive in the mail.

> **TIP:** Sometimes software packages will be available in both libc5 and libc6 formats. This designation refers to the version of C programming-language libraries used by the application. If you have a choice, choose the libc6 packages. These are compatible with Red Hat Linux 7 and later (or any Linux kernel version 2.2 and higher). In fact, all major Linux distributions now use libc6. Better yet, look for packages designated for the specific distribution you are using (such as Fedora, Red Hat Linux 9, and so on).

You can visit FTP sites containing RPM packages if you already have some idea of what you are looking for. You can start by reading the README and INDEX files for a particular software product to get your bearings. When you find the software you want, simply click the link to begin downloading the software to your computer. Here are a few sites that are particularly good for finding RPM packages:

- **Rpmfind** (www.rpmfind.net) — Open source software that is already packaged up in Red Hat Package Management (RPM) format is available from this site. Do a keyword search from this Web site, then download the appropriate RPM from the search results.
- **FreshRPMs** (www.freshrpms.net) — Another site with a good selection of high-quality RPMs.
- **Red Hat FTP Mirrors** (www.redhat.com/mirrors.html) — Go to this page for a listing of FTP sites containing Red Hat software that you can download. Most of these sites also have a variety of freeware and shareware applications that are usable with Linux.

Often, you can't just download a single software package to get the software in that package to work. Many packages depend on other packages. For example, software packages for playing audio and video typically rely on other software packages for decoding different kinds of content. To deal with this issue, Red Hat Linux (Fedora Core) has included the yum package.
