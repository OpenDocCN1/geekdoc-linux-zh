# **Chapter 5: Accessing and Running Applications 223**

> **TIP:** If you want to migrate your desktop systems from Windows to Linux, you can start by moving to cross-platform systems that run on both Windows and Linux. For example, move from Microsoft Office to OpenOffice.org. Move from Internet Explorer to Firefox and from Outlook to Thunderbird. If you do this, you will substantially ease the final migration to Linux.

Although not an open source product, Win4Lin is another good way to run Windows applications, along with a Linux system on the same running computer. With the open source QEMU project, you can simultaneously run Microsoft Windows and Linux operating systems on the same PC. (Go to `http://www.nongnu.org/qemu/` and click on Status for a complete list of supported operating systems.)

In general, Windows applications are less likely to break in QEMU than they are in WINE (because you actually run the whole Windows operating system), but performance may not be as good (because you run an operating system within an operating system). See Chapter 25 for more on QEMU. The next section describes how to set up Linux to run Microsoft Windows applications using WINE.

# Running Windows Applications with WINE

For WINE to let you run Microsoft Windows applications, it needs to have an environment set up that looks like a Microsoft Windows system. The following section takes you through the steps of installing and configuring the wine RPM available from Fedora. You can install WINE from the Fedora yum repository by typing the following:

```
`# yum install wine wine-core wine-docs`
```

Although you only need the wine and wine-core packages, wine-docs offers some useful documents in the `/usr/share/doc/wine-docs*` directory for developing software and using WINE. The `yum command line` just shown will also pull in other WINE packages from the Fedora repository (such as those that include additional support for sound, scanners, and other features mentioned earlier).

The location of the basic Microsoft Windows operating-system directories for WINE is the `$HOME/.wine/drive_c` directory for each user, which looks like the `C: drive` to WINE. The `$HOME/.wine` directory is created automatically in your home directory the first time you run `Wine Configuration` (select Applications \(arrow\) Wine \(arrow\) Wine Configuration) or type the `winecfg` command:

```
`$ winecfg`
```

This opens the Wine configuration window, where you can do most of your activities to add applications, configure the operating system, and integrate with the desktop. Figure 5-5 shows an example of the Wine configuration window.