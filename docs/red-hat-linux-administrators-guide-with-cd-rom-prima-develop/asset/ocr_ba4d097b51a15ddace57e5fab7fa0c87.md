# Adding Tools for Audible Entertainment

Now that you have a functioning sound card and can pipe sound files from your hard drive to speakers or audio devices, you can begin thinking about playing other forms of sound files on your own system. This section covers the installation and configuration of other useful tools that will allow you to play audio files for your own entertainment.

Linux provides a host of configurable CD or sound players that either come pre-installed with the distribution CD or are available for download. Many are designed specifically for use with a particular window manager but can be played on any interface of your choice. They may have options particular to that specific window manager. You can easily ignore, shut off, or optimize these sound players for the window manager depending upon how closely the sound programs are interrelated.

# Choosing CD Players

Some of the most basic CD players come with the basic Red Hat distribution. The XPlayerd program is a standard component on most all Red Hat releases. It plays regular audio CDs on all ATAPI CD-CD-ROMs without any need to mount the media or reconfigure the device. With older Red Hat releases, you may have to allow yourself access to the device. Under older Red Hat releases you may have to grant yourself access to the CD-ROM by typing the following command as root. Otherwise, the CD-ROM should be accessible to any user:

```
# chmod 666 /dev/cdrom
```

This command enables you and any other users to read files from the CD-ROM.

Both Gnome and KDE offer their own CD players as well. You can call up Gnome by executing gved at the command line. Or, if you are within the Gnome desktop, you can select the CD player from under the Multimedia tab. Likewise, you can execute KDE's CD player, kscd, from within any window manager. Both have CDDb support--that is, if the host machine has Internet access, they can query any of the many CDDb ( CD Databse) servers and download additional information about the artist, CD title, and titles of the songs on the CD. You can either store these facts locally for later use or download them the next time the CD is installed.