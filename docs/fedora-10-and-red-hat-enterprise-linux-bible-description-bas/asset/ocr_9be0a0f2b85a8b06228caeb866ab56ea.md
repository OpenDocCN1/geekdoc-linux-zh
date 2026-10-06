# Chapter 8: Music, Video, and Images in Linux 319

Media tab. Then from the Media tab, select the box next to CD Audio and select to either ask what to do or nothing when an audio CD is encountered.

# Troubleshooting Your CD-ROM

If you are unable to play CDs on your CD-ROM drive, here are a few things you can check to correct the problem:

+   * Verify that your sound card is installed and working properly (see “Configuring a sound card” earlier in this chapter).
* Verify that the CD-ROM drive was detected when you booted Linux. If your CD-ROM drive is an IDE drive, type `dmesg | grep -i cd`. You should see messages about your CD-ROM that looks like `ata2:0: ATAPI: HL-DT-ST-RW/DVD DRIVE GCC-424N, 0201, max UDMA/33`.
* If you see no indication of a CD-ROM drive, verify that the power supply and cables to the CD-ROM are connected. To make sure that the hardware is working, you can also boot to DOS and access the CD.
* Try inserting a CD-ROM. If you are running the GNOME or KDE desktop, a desktop icon should indicate that the CD is mounted by itself. If no icon appears, go to a Terminal window and mount `/media/cdrecorder`. Then list the contents using it. This tells you if the CD-ROM is accessible.
* Check that your CD-ROM drive is not blacklisted because of buggy firmware or other issues. See www.tlid.org/HOWTO/Hardware-HOWTO/cdrom.html.
* If you get the CD-ROM working, but it fails with the message CDROM device: Permission denied when you try to play music as a nonroot user, the problem may be that the device related to medium is not readable by anyone but root. Type `grep media` to see what device name represents the drive. If were `/dev/scd0`, type `chmod 644 /dev/scd0` to enable all users to read it. One warning: If others use your computer, they will be able to read any CD you place in this drive.

# Playing and managing with Rhythmbox

Rhythmbox is a tool for gathering, managing, and playing your music collection from one application. It lets you import music (from a CD, URL, or folder), and then select and sort your music by album, artist, title, or other variables. Rhythmbox also lets you play Internet stations.

The first time you run Rhythmbox, consider setting some Rhythmbox Preferences by selecting Edit → Preferences. On the Music tab, you can tell Rhythmbox the folder in which to store