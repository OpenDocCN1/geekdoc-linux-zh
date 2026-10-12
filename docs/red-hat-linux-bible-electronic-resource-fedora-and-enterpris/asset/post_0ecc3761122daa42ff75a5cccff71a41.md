
Figure 6-13: GIMP is a powerful tool for graphic manipulation.

![](img/27a85d56d393921ced6412ae6e8336bf_260_0.png)

> **NOTE:** If GIMP is not on your system or is not installed properly, you can install it from CD #1 that comes with this book. Alternatively, you can obtain the latest copy of GIMP from www.gimp.org.

In many ways, GIMP is similar to Adobe Photoshop. Some people feel that GIMP’s scripting features are comparable to, or even better than, Actions in Adobe Photoshop. One capability that GIMP lacks, however, is support for CMYK separations.

### Taking screen captures

If you want to show examples of the work you do on Red Hat Linux, you can use the Screen Capture program to capture screen images. (The ksnapshot command is part of the kdegraphics package contained on CD #2.)

To open Screen Capture, from the Red Hat menu click Graphics → Screen Capture Program (or type ksnapshot). Figure 6-14 shows an example of the Screen Capture program.

When Screen Capture first opens, it takes a snapshot of the full desktop. Buttons on the window let you:

- **Print Snapshot** — Have the snapshot sent to your printer.
- **Save Snapshot** — Save the snapshot to a file in X bitmap, windows icon, PNG, portable pixmap, JPEG, X pixmap, Encapsulated PostScript, or Windows BMP formats.
- **New Snapshot** — Take a new snapshot. With "Only grab the window..." selected, you can click a window to capture that window alone.

![](img/27a85d56d393921ced6412ae6e8336bf_261_0.png)

### Modifying images with KPaint

Using the KPaint window, a utility that comes with KDE (in the kdegraphics package on CD #2), you can work with and convert images in several formats. Figure 6-15 shows an example of KPaint.

![](img/27a85d56d393921ced6412ae6e8336bf_261_1.png)

Start KPaint from either the desktop (from the Red Hat menu, click Graphics → More Graphics Applications → Paint Program) or from a Terminal window (`/usr/bin/kpaint&`). Start with either a blank canvas or by opening an image in one of the supported formats (File → Open, browse for a file, and then select OK). Look in the /usr/share/backgrounds directory for graphics to try.

The painting tools let you draw ovals, boxes, lines, and other shapes. You can save the file to several different formats, including MS Windows pixmaps, Encapsulated PostScript image, MS Windows icons, JPEG, PNG, PNM, TIFF, X bitmap, or X Window pixmap.

### Using Scanners Driven by SANE

Software for using a scanner with Linux is being driven by an effort called Scanner Access Now Easy (SANE). This effort hopes to standardize how device drivers for equipment such as scanners, digital still cameras, and digital video cameras are created, as well as help simplify the interfaces for applications that use those devices.

SANE is now included with the Red Hat Linux distribution. The sane-backend and sane-frontend packages are on CD #1, while the xsane and xsane-gimp packages are on CD #2. You can get the latest SANE driver packages from www.mostang.com/sane.

Someone wanting to use Linux as a publishing platform is generally interested in two issues about scanners: which scanners are supported and which applications are available to use the scanners. In general, more SCSI scanners are supported than parallel scanners.

Because of the ongoing development effort, new scanners are being supported all the time. You can find a current list of supported scanners at www.mostang.com/sane/sane-backends.html. As for applications, these are currently available with Red Hat Linux:

- **xsane** — This is an X-based graphical front end for SANE scanners; xsane can work as a GIMP plug-in or as a separate application (from the Red Hat menu, select Graphics → Scanning). It supports 8-bit output in JPG, TIFF, PostScript, and PNM formats. There is experimental 16-bit support for PNM (ASCII), PNG, and raw formats.
- **scanimage** — This is a command-line interface for obtaining scanned images. It supports the same formats as xscanimage. The command acquires the scanned image, and then directs the data to standard output (so you can send it to a file or pipe it to another program).

Because of the architecture of SANE scanner drivers, it is possible to separate scanner drivers from scanner applications. This makes it possible to share scanners across a network.

### Summary

In recent times, modern GUI-based publishing tools have augmented the text-based publishing tools that have always been available with Red Hat Linux (and other UNIX systems). Powerful open-source publishing tools such as OpenOffice are becoming competitive with commercial office suites. Traditional publishing tools such as Groff (which implements traditional troff/nroff text processing) and LaTeX (a TeX macro interface that is particularly suited for scientific and mathematical publishing) are still available with Red Hat Linux.

## Chapter 7: Playing Games with Red Hat Linux

**In This Chapter**

- Basic Linux gaming information
- X Window games
- Commercial Linux games
- Transgaming and WineX gaming

The advancement of computer games has mirrored the improvements in computers themselves. In the 1970s, the first games for UNIX systems were visually simple and could run on slow, character-based terminal connections. Today, games that combine graphics, animation, and sound have helped drive improvements in computer technology in general.

Availability of gaming software useable with Red Hat Linux is similar to that of Linux publishing software. A lot of the old software is still around (and is free), while newer software is available in demo form but costs some money to get a full version. Some experts predict that gaming will be the software category that brings Linux into homes. Although the number of popular game applications is limited at the moment, like everything else in Linux, more are becoming available each day.

This chapter addresses the current state of gaming in Linux, including the basics on getting your gaming environment going, and hardware considerations for gaming. It describes the free games (mostly fairly simple X Window games) that come with Red Hat Linux or that can be easily downloaded. For running games that were created for other platforms, this chapter describes game emulators such as WineX.

This chapter also discusses some popular commercial games that have demo versions available for Linux. If you like the demos, you can purchase these games, which run natively in Linux.

### Basic Linux Gaming Information

### Where to get information on Linux gaming

To find news on the latest games available for Linux, as well as links to download sites, go to some of the several Web sites available. Here are a few to get you started:

- **TransGaming Technologies** (www.transgaming.com) — This company’s mission is to bring games from other platforms to Linux.
- **The Linux Game Tome** (http://happypenguin.org) — This site features a database of descriptions and reviews of tons of games that run in Linux. You can do keyword searches for games listed at this site. The site also includes links to where you can get the different games, as well as links to other gaming sites.
- **Linuxgames.com** (http://linuxgames.com) — This site can give you some very good insight into the state of Linux gaming. There are links to HOW-TOs and Frequently Asked Questions (FAQs), as well as forums for discussing Linux games. There are also links to Web sites that have information on a particular game you are interested in.
- **id Software** (www.idsoftware.com) — Go to the id Software site for information on Linux demo versions for Quake, Unreal Tournament, and Return to Castle Wolfenstein.
- **Loki Entertainment Software** (www.lokigames.com) — Loki provided ports of best-selling games to Linux, but went out of business in 2001. Its products included Linux versions of Civilization: Call to Power, Myth II: Soulblighter, SimCity 3000, Railroad Tycoon II, and Quake III Arena. The Loki Demo Launcher is still available to see demo versions of these games, and some boxed sets are available for very little money.
- **Tux Games** (www.tuxgames.com) — If you are ready to purchase a game, the Tux Games Web site is dedicated to the sale of Linux games. Besides offering Linux gaming news and products, the site lists its top-selling games and includes notices of games that are soon to be released.
- **Linux Gamers' FAQ** (http://iculus.org/lgfaq) — This FAQ contains a wealth of information about free and commercial Linux games. It lists gaming companies that have ported their games to Linux, tells where to get Linux games, and answers queries related to common Linux gaming problems.

If the idea of developing your own games interests you, try the Linux Game Development Center (http://lgdc.sunsite.dk).

### Getting started with Linux gaming

How you get started with Linux gaming depends on how serious you are about it. If all you want to do is play a few games to pass the time, you can find plenty of diverting X Window games that come with Linux. If you want to play more powerful commercial games, you can choose from:
