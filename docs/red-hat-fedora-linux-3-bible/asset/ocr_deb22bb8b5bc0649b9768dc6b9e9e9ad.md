cables to the CD-ROM are connected. To make sure that the hardware is working, you can also boot to DOS and try to access the CD.

+   - Try inserting a software CD-ROM. If you are running the GNOME or KDE desktop, a desktop icon should appear indicating that the CD mounted by itself. If no such icon appears, go to a Terminal window and type mount /media/cdrecorder. Then change to the /media/cdrecorder directory and list the contents using the command cd /media/cdrecorder; ls. This tells you if the CD-ROM is accessible.

+   - If you get the CD-ROM working, but it fails with the message "CDROM device: Permission denied" when you try to play music as a nonroot user, the problem may be that device related to that medium is not readable by anyone but root. Type mount | grep media to see what device name represents the drive. Then (as the root user), if, for example, the CD device were /dev/hdc, type chmod 644 /dev/hdc to enable all users to read your CD-ROM and to enable the root user to write to it. One warning: if others use your computer, they will be able to read any CD you place in this drive.

# Playing CDs with gnome-cd

Like most graphical CD players, the gnome-cd player has controls that look similar to what you would see on a physical CD player. If you are using the GNOME desktop, from the System Menu select Sound & Video → CD Player, or from a Terminal window, type:

```
```
$ gnome-cd &
```
```

If your computer is connected to the Internet, then for most CDs, you'll see the title and artist information. Even obscure artists are represented in the free online databases. If the information isn't available, you can enter it yourself.

The interface for adding information about the CD and its tracks is very nice. Click the Open Track Editor button. You can add Artist and Title information over the CD. Then you can select each track to type in the track name. To add the name of the artist and the disc title, click in the appropriate text box and type in that information. Figure 8-2 shows the CD Player and the CDBB Track Editor.