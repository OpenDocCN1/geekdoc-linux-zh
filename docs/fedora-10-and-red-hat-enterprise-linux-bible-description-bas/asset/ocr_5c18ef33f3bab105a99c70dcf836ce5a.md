# Chapter 5: Accessing and Running Applications 235

applications is growing, and special attention is being paid to getting important Windows and XP applications running.

Although not an open source product, Win4Lin is another good way to run Windows applications, along with a Linux system on the same running computer. With the open source QEMU project you can simultaneously run Windows and Linux operating systems on the PC. (Go to http://bellard.org/qemu/status.html and click on List of Supported Guest OSEs for a complete list of supported operating systems.)

In general, Windows applications are less likely to break in QEMU than they are in Wine (since you actually run the Windows operating system), performance may not be as good (good since you run an operating system over another operating system). The next section describes how to set up Linux to run Microsoft applications using Wine.

# Running Windows Applications in Wine

For Wine to let you run Windows applications, it needs to have an environment set that looks like a Microsoft Windows system. The following section takes you through the steps of installing and configuring the Wine RPM available from Fedora. You can install wine over the Internet by typing the following:

```
# yum install wine-tools wine-core wine-docs
```

Although you only need the wine and wine-core packages, wine-tools offers some useful graphical tools for working with your WINE environment and wine-docs offers some useful documents in the /usr/share/doc/wine-docs* for developing software and using WINE. The yun command line shown above will also pull in other wine packages from the Fedora repository (such as those that include additional support for sound, scanners, and other features mentioned earlier).

The location of the basic Windows operating-system directories for WINE is the $HOME/.wine/drive_c directory for each user, which looks like the C: drive to wine. The $HOME/.wine directory is created automatically in your home directory the first you run Wine Configuration (select Applications $ightarrow$ Other $ightarrow$ Wine $ightarrow$ Wine Configuration) or type the winecfg command:

```
$ winecfg
```

This opens the Wine configuration window, where you can do most of your activities to add applications, configure the operating system, and integrate with the desktop. Figure 5-5 shows an example of the Wine configuration window.