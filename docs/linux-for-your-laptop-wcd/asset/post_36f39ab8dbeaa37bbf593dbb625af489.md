
## Command-Line Utilities

To mount, read, create, and write CD-ROM images, you'll need several Linux utilities: `mkisofs` to create an ISO image on your hard drive to hold the CD's contents, `mount` to mount an existing CD-ROM as an ISO image, `dd` to copy a CD's contents, `mke2fs` to format blank hard drive image files, and `cdrecord` to write selected files or write an ISO image to your CDR or CDWR drive. Note that before you begin, you might need up to 1.4GB of free hard drive space!

For example, one way to make a quick copy of a data CD-ROM (such as a bootable Linux CD) is to first use the `dd` command to copy the CD:

```
# dd if=/dev/scd0 of=cimage
```

You can then write the image with the `cdrecord` command, specifying your CDR or CDWR drive like this:

```
# cdrecord -v speed=2 dev=0,1,0 -data cimage
```

This will copy the file `cimage` onto your blank CDR or CDWR disk in the SCSI drive with an ID of 1 on bus 0. If your CDR or CDWR drive is fast enough, you can use a faster speed= setting. If you downloaded an ISO image of a CD-ROM, you can mount the image locally (and access its files and directory structure) like this:

```
# mount -t iso9660 -o loop=/dev/loop1 cimage /mnt/cdrom
```

This command will mount the CD-ROM's image file under the `/mnt/cdrom` directory as if it were an inserted CD-ROM. You can then copy the files from `/mnt/cdrom` to a new directory, such as `/mnt/cdrom_new`, to change the files or fix any problems. You can then create a new ISO image from the new directory by using the `mkisofs` command and specifying the new `/mnt/cdrom_new` directory like this:

```
# mkisofs -r -o new_cimage /mnt/cdrom_new
```

You can then write the new image to create a new CD-ROM. There are special tricks and steps you need to take to write audio CDs, to mix and match audio tracks to create custom CDs of .mp3 files, or to back up your notebooks’ hard drive directly to a backup CD. See the CD-Writing HOWTO under the /usr/doc/HOWTO directory for details (or browse to http://www.linuxdoc.org).

## Graphical Interface Clients

Again, just as you can use the command line to copy, create, and write CDR and CD-RW disks, life gets much easier when you use a graphical interface client to do all the hard work. One of the best programs to use with Linux to create CDRs and CDRW drives is X-CD-Roast. You’ll find this X11 software package (a front end to the utilities discussed previously) included with nearly all modern Linux distributions.

Start the client from the command line like this:

```
# xcdroast &
```

When you start the program for the first time, you’ll be asked to enter xcdroast’s setup dialog box shown in Figure 18.16.

Click on xcdroast’s Setup tab to designate your CD-Writer and CD-Reader devices. This client is even more efficient when you use it on a notebook with two CD-ROMs (internal and external). You’ll also need to designate temporary hard drive space and an image mount point. If you want to verify audio tracks, you need to make sure Linux is configured to work with your notebook’s sound system.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_434_0.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_435_0.png)

Figure 18.17 Verify the data CD's info, and then click on the Read Image button to copy the CD.

When you've finished your setup, click the Save button, and then click the Done button. You'll then return to the main xcdroast window.

To copy a data CD, insert the CD into your drive, and then click on the Copy Data CD button in the main xcdroast window. You'll see the dialog box shown in Figure 18.17.

Click on the Read Image button to copy the CD. Its contents will be saved according to the default paths you specified when you set up xcdroast. Next, click on the Start Read Image button, shown in Figure 18.18.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_435_1.png)

Figure 18.18 Click on the Start Read Image button to start copying your CD.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_436_0.png)

Figure 18.19 The xcdroast client will read the contents of your CD and create an image file on your hard drive.

The CD's contents (in this example, on 31MB because the CD is a "business card" CD) will be read and saved. This process can take quite some time, depending on the amount of data on your CD. When the read is finished, click on the OK button to continue, as shown in Figure 18.19.

In the main dialog box, you can then click on the Verify Image button. The xcdroast client will compare the contents of the copied CD with the image file saved on your hard drive. When you're satisfied, remove the original CD, and then insert a blank CDR or CD RW disk. Next, click on the Write Image button to start copying the image onto your new CD. As before, you'll see a dialog box with the CD's info, but this time, instead of Start Read Image (as shown in Figure 18.18), the button's name is Start Write Image, as shown in Figure 18.20.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_436_1.png)

Figure 18.20 Click on the Start Write Image button to write your new CD.

Note that you'll also be prompted to insert the blank CD. Click on the button to start writing your CD. Note that this process can take even longer than reading a CD image onto your hard drive! No CD writer drives on the market have a faster write than read speed.

The xcdroast client has many other features, and it can be used to directly copy data from one CD to another. Another great feature is the ability to “master” a CD by collecting data in a specified directory and then writing the data to CD-ROM. This is a great way to copy nearly 10 CDs of audio music (.mp3 files) onto one CD-ROM! Be sure to read xcdroast's manual and document to make the most out of your burning sessions.

## Resource Information

- http://promo.net/pg/
  The home page for Project Gutenberg, where thousands of free books are available for download.
- ftp://metalab.unc.edu/pub/Linux/games/
  The source for the original text-only BSD games.
- ftp://metalab.unc.edu/pub/Linux/games/strategy
  The source for the LinCity simulation game.
- http://linuxberg.ozbytes.net.au/x11soft.html
  A comprehensive index of Linux software, including arcade games.
- http://www.torque.net/linux-pp.html
  The Linux parallel port home page. It has many links to documents and software to help you use a parallel-port device with Linux, including support for ATAPI CDR and CDWR drives.
- http://www.gnug.de/wnini/cdr/html/
  Winfried Trumper’s CD-Writing HOWTO. It’s a compendium of tips and tricks on using Linux to copy, collate, and duplicate audio tracks and data onto CDR or CDWR disks.
- http://www.linuxdoc.org/HOWTO/Sound-HOWTO.html
  A link to Jeff Tranter’s comprehensive Sound-HOWTO.

### SUPPORTED.CARDS

David Hinds' list of currently supported PC cards for use with Linux. It can be found under the `/usr/doc/pcmcia*` or `/usr/src/pcmcia*` directories. It also can be found at `http://pcmcia.sourceforge.org/`.

- http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html
  The home page for the cdrecord utility.
- http://krabber.automatix.de/
  The krabber client home page. It's one of the best X11 KDE clients for ripping .mp3s from audio CDs.
- http://www.fh-muenchen.de/home/ze/rz/services/projects/xcdroast/xcdr098/
  Thomas Niederreiter's home page for the xcdroast client for X11 and Linux. You can also find the software at http://www.fh-muenchen.de/rz/xcdroast/.
