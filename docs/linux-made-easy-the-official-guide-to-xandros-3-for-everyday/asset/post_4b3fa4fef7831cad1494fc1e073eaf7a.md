
gone the way of the dodo, great auk, and Carolina parakeet. In fact, not only do they continue to be used, but the range of removable storage media available to us has actually expanded to include Zip disks, DVDs, and, more recently, USB hard disks, flash drives, and memory card readers.

Given the diverse ways in which people use their computers today, being able to use these various forms of hard storage media has thus become more or less essential. Whether it be for importing photos from your digital camera, listening to music and watching movies on your computer, or just backing up all the valuable items you have stored on your hard disk, you eventually will have to deal with at least some of the various forms of hard media available in the computer world today.

Fortunately, the Xandros File Manager makes this all quite easy by acting as a port of sorts (hence the title of this chapter—hard stretch, I know), from which you can easily load and unload data to and from the various media that drop anchor at your machine. Whether you insert floppy disks, CDs, or DVDs into their respective drives or connect any other storage device to one of your USB ports, you will be able to access those media via the Xandros File Manager.

### Floppies

When the original Macintosh computer first came out, one of the coolest things about it was that it used 3.5-inch floppy disks (also known as *floppies*). At the time, I thought that those disks, with their hard casing and sliding metal doors protecting the media itself, were the incarnation of high-tech cool. Times change, of course, and there are fewer and fewer people using floppies these days.

The reason for this change is simple: files have just gotten too big for floppies. The audio, video, and image files most people deal with these days are gigantic. You’d be lucky, for example, to fit more than three digital photos on one floppy disk. Compared to CDs, Zip disks, memory cards, and the like, floppies are also too slow. You could practically feed the cat, make a cup of coffee, and read the first three pages of the newspaper in the time it takes to write a good number of files to a floppy. (Well, okay, that’s an exaggeration, but floppies are slow when compared to the alternatives.)

Despite being small and slow, floppies are still used by a dwindling number of people who have no other way of transferring files to removable media, or who just want to hand over one or two small word processing documents to another person who can read no other type of media. You may be one of these people, or you may have to send files to or receive them from someone in this situation.

### Writing to and Copying from Disk

Using floppies on your system is easy enough: just insert the floppy into its drive, open XFM, and then click the **Floppy** icon near the bottom of the file tree in the left pane of the window. The contents of the floppy will appear in the right pane. To copy, add, or remove files to or from the floppy, use the various methods I described in Chapter 5, and immediately the data will be written to (or removed from) the disk. When you have finished, eject the floppy manually.

> **NOTE**
> *When you remove a floppy from the drive, the files displayed in the right pane of the XF M window will remain. This is a temporary state of affairs, however, so don't worry. Just click any other folder in the file tree until the contents of that folder are displayed in the right pane. After that, just click the Floppy icon in the file tree again, and the files previously displayed there will be gone.*

### Formatting Floppies

Before you can actually write anything to a disk, that disk must be formatted. This is true of any kind of storage media—your hard disk, CDs, storage cards for your digital camera, or floppy disks—though it is sometimes done before you buy the media. By formatting a disk, your system (at your request) lays down a sort of map on the disk that specifies where data can be stored.

> **NOTE**
> *Because there are, and have been, many operating systems, there are many such formats for floppy disks. Linux can read both Linux-native ext2 formatted disks and Windows / DOS FAT formatted disks. It can also create either format.*

Most floppy disks these days are sold preformatted in DOS format, so you probably don't have to worry much about this; however, if you do need to format an unformatted floppy disk, or even an already used one from which you want to erase all the data, the process is simple.

- 1. Insert the floppy into its drive, and then open the Xandros File Manager. Click the **Floppy** icon in the file tree of that window, and then click the words **Format Floppy** at the left side of the right pane of the window. A Floppy Disk Formatter window should appear, as shown in Figure 6-1.

![](img/3badae5570de77b990135448f8a8a1cc_110_0.png)

*Figure 6-1: Formatting a floppy disk*

- 2. In this window, you can specify the density, or capacity, of the floppy (1.44 MB or 720 KB), the file system type (ext2 or FAT), and the name for the disk. Once you have done so, begin formatting the floppy by clicking the Format button.
- 3. A small window will appear asking if you are sure you want to proceed. Click Continue and the formatting process will begin, with its progress indicated at the bottom of the Floppy Disk Formatter window.
- 4. When the process is complete, another window will appear telling you so. Just click OK on that window, and the process will be complete.

### Reading Data CDs or DVDs

To read a CD or DVD with data on it (images, files, or programs) rather than music, place the disc in your CD or DVD drive. A Xandros File Manager window should automatically open and display the contents of the disc. You can then copy the files on the data CD or DVD to your hard disk using the copy-and-paste or drag-and-drop methods described in Chapter 5.

> **NOTE**
> *As I mentioned in Chapter 5, any file that you copy from CD or DVD to your hard disk will be write-protected, so you will have to change its permissions if you want to alter it. To do so, right-click the file, select Properties in the pop-up window, and then click the Permissions tab in the Properties window and change the permissions.*

When you have finished copying files from the CD or DVD, you can eject it by right-clicking the icon that says DVD-ROM or CD-RW and selecting Eject Disk in the pop-up menu.

### Playing Music CDs

To play a music CD, insert it into your drive; the Kscd CD player (shown in Figure 6-2) should open automatically and begin playing it. You should also see a small applet in the Panel that looks like a small CD with a pair of quarter notes on it (also shown in Figure 6-2), which you can use to hide or show the player and control its basic functions. If you are connected to the Internet and playing a commercial audio CD, Kscd will also query an online database (freedb.org) in order to gather album and track titles, which it will then display in the player window.

When you have finished playing your CD, you can eject it by clicking the Eject button in the player window or by right-clicking the Panel applet and selecting Eject in the pop-up menu.

> **NOTE**
> *Closing the Kscd player window does not close the Panel applet. To do so, right-click the applet, and then select Quit in the pop-up menu. Doing this without first closing the player window will accomplish both tasks in one step.*

![](img/3badae5570de77b990135448f8a8a1cc_112_0.png)

Figure 6-2: The Kscd player and Panel applet

### Playing DVD and VCD Videos

If you have a DVD drive, Xandros can also play unencrypted DVDs via its bundled video playback software, Xine (Figure 6-3). Xine can also play VCDs (video compact discs), which are movies recorded on specially formatted CDs that can be played in DVD or CD drives. VCDs are inferior to DVDs in terms of image quality, but they are much cheaper. Because they are popular mainly in China (especially Hong Kong) and a few other countries, however, you might not come across many of them unless you happen to love more obscure Chinese movies or Canto-pop karaoke. Still, if you do run across any, you will be pleased to know that you can play them.

![](img/3badae5570de77b990135448f8a8a1cc_112_1.png)

Figure 6-3: Viewing DVDs and VCDs with Xine
