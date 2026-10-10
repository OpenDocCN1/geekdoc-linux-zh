CD-ROM drives (as well as your other removable media, such as DVDs and digital cameras) and opens a CD player when it sees an audio CD.

If you don't want to have CDs automatically start playing or if you want to use a different CD player by default, you can change that behavior using the GNOME Volume Manager's Removable Drives and Media Preferences window. Select System \u2192 Preferences \u2192 Hardware \u2192 Removable Drives and Media. Then from the Multimedia tab, either turn off the Play audio CD selection or change the command that is run (for example, to gnome-cd \u00a7d).

Refer to the "Managing removable media (CDs, DVD, and cameras)" section of Chapter 3 for details on using the GNOME Volume Manager to change CD playing and mounting preferences.

# Troubleshooting Your CD-ROM

If you are unable to play CDs on your CD-ROM drive, here are a few things you can check to correct the problem:

+   - Verify that your sound card is installed and working properly (see "Configuring a sound card" earlier in this chapter).

+   - Verify that the CD-ROM drive was detected when you booted Linux. If your CD-ROM drive is an IDE drive, type `dmseg | grep "hd.` You should see messages about your CD-ROM that look like this: hdc: CD-ROM CDU701, ATAPI CDROM drive; or this: hdc: ATAPI 14X CD-ROM drive, 128KB Cache.

+   - If you see no indication of a CD-ROM drive, verify that the power supply and cables to the CD-ROM are connected. To make sure that the hardware is working, you can also boot to DOS and try to access the CD.

+   - Try inserting a software CD-ROM. If you are running the GNOME or KDE desktop, a desktop icon should appear indicating that the CD is mounted by itself. If no such icon appears, go to a Terminal window and type `mount /media/cdrecorder`. Then list the contents using the `ls /media/cdrecorder` command. This tells you if the CD-ROM is accessible.

+   - Check that your CD-ROM drive is not blacklisted because of buggy firmware or other issues. See www.tldp.org/HOWTO/Hardware-HOWTO/cdrom.html.

+   - If you get the CD-ROM working, but it fails with the message `CDROM device: Permission denied` when you try to play music as a nonroot user, the problem may be that the device related to that medium is not readable by anyone but root. Type `mount | grep media` to see what device name represents the drive. Then (as the root user), if, for example, the CD device were `/dev/scd0, type chmod 644 /dev/scd0` to enable all users to read your CD-ROM and to enable the root user to write to it. One warning: If others use your computer, they will be able to read any CD you place in this drive.