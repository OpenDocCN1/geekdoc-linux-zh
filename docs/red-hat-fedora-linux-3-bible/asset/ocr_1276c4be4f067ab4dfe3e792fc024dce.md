```
smb://ESTREET;christoys/toyprojects
```

Here are a few things you should know about accessing Samba shares from Mac OS X:

+   When authenticating your password (see Figure 26-4), Mac OS X sends your password in clear text. Unlike when authenticating an AppleTalk share, there is no way to select to send encrypted passwords from this window.

+   The example of setting up Linux Samba shares in Chapter 18 shows how to set up Samba to ask for encrypted passwords (and therefore will fail authentication from Mac OS X). To get around the problem (on a secure network), you can create a share that either accepts clear-text passwords or have the share be available to guest users.

> NOTE: To configure a particular Samba share to work from a Mac OS X client, you can edit the `/etc/samba/smb.conf` file (as root user). In a shared directory definition, add the line `guest ok = yes` (to allow guest users access to the share) or `encrypt passwords = no` to accept clear-text passwords.

# Sharing X applications

Most UNIX-like computer systems rely on the *X Window System* (also referred to as *X11* or simply *X*) to display graphically-based windows over a network. Sharing applications over the network with X requires little more than having X running and making it accessible to displays that are directed to your display (see Chapter 3 for information on launching X applications).

Although the default graphical interface for Mac OS X is a facility called Aqua, there is now an X11 for Mac OS X available for Mac users. The latest version of Mac OS X, nicknamed *Panther*, includes a native *X* installation. You must choose a Custom install or upgrade when you install Panther to get the X packages on your system. For further information on the state of the *X Window System* in Mac OS X, or to download your own copy of X11 for Mac OS X, go to `www.apple.com/macosx/features/x11`.

With X11 installed and running on your Mac OS X, you can launch X applications from your Linux system and have them appear on your Mac OS X desktop.

# Configuring an AppleTalk Server in Linux

If you have a mixture of older Macs (such as a Power Macintosh with Mac OS 8.1) and newer Macs (such as an iMac with Mac OS X) on the same LAN, an AppleTalk server could be the best way to share files and printers among them. With the *netatalk* package installed on your Fedora server, *netatalk* can be configured to act as that AppleTalk server.

Using *netatalk*, you can allow multiple Mac clients to use the following features from a computer running Fedora:

+   **AppleShare file server** — Files and directories you share from your AppleTalk server (via *netatalk*) are stored with features and permissions that a Mac user would expect.