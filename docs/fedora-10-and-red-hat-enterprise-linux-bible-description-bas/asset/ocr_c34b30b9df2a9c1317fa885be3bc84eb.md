# Chapter 26: Integrating Fedora with Apple Macs 991

```
$ export DISPLAY=10.0.0.50:0
```

+   4. From this Terminal window on the Fedora system, launch any Application by typing its name. For example, to run a clock program (xclock), type the following:

```
$ xclock
```

The clock application will appear on the desktop of the Mac OS X system. You can run any X11 application you like from Terminal window in Fedora to have it appear on the Mac's desktop.

# Configuring an AppleTalk Server in Linux

If you have a mixture of older Macs (such as a Power Macintosh with Mac OS 8.1) and newer Macs (such as an iMac or Mac Mini with Mac X) on the same LAN, an AppleTalk server could be used to share files and printers among them. With the netatalk installed on your Fedora server, netatalk can be configured to act as that AppleTalk server.

Using netatalk, you can link multiple Macs to use the features from a computer running Fedora:

+   * **AppleShare file**— Files and directories you share from your AppleTalk server (via netatalk) are stored with features and permissions that a Mac user would expect.
* **AppleTalk printer server**— Printers configured on your Linux server can be shared as though they were AppleTalk printers.
* **AppleTalk router**— Your Linux system can act as a router between multiple AppleTalk networks.

The netatalk project site is located at http://netatalk.sourceforge.net. There, you can find documentation (including an FAQ), as well as links to help netatalk Web sites.

To use netatalk in its most basic configuration, all you need to do is:

+   * Create a LAN connecting your Linux server and Mac clients. You can configure netatalk as a router to connect multiple LANs.
* Start netatalk as described in the "Starting netatalk" section. This enables any users with user logins to your Linux computer to access their home directories from a Mac (using Linux logins and passwords). You can also add printers and other directories to share.

Before you fire up netatalk, I recommend that you check out the following section.

# Before you start using netatalk

Know that when you are creating an AppleTalk server on a Linux file system, you are creating a hybrid-type file system. Strange issues can arise because the two types of servers handle ownership, access, and file attributes (such as what applications launch a file) differently.