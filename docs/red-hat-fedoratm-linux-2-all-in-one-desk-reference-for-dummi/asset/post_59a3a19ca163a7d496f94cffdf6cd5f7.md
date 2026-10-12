
## Joining the BitTorrent

![](img/9f89727199836b0f871f1745838aa8b2_127_0.png)

If you don't find the correct BitTorrent RPM file at `torrent.dulug.duke.edu/btrpms/`, you can always download the files from the official BitTorrent home page at `bitconjurer.org/BitTorrent/`. For example, to download and install BitTorrent 3.3, open a terminal window and type the following commands:

```
wget http://bitconjurer.org/BitTorrent/BitTorrent-3.3.3.tar.gz
tar -xzf BitTorrent-3.3.3.tar.gz
```

In this case, the BitTorrent software is installed in the BitTorrent-3.3 subdirectory of the current directory and you have to run the BitTorrent client from that subdirectory.

## Open incoming TCP ports used by BitTorrent

Typically, your system runs a firewall that restricts access to many of the ports. BitTorrent, however, requires that you open up the TCP ports numbered 6881 through 6999 so that other BitTorrent clients can contact your system and request uploads. To open TCP ports 6881 through 6999, type the following command in a terminal window:

```
iptables -I RH-Firewall-1-INPUT --protocol tcp --dport 6881:6899 -i eth0 -j ACCEPT
```

This command assumes that your system connects to the Internet through its Ethernet interface and that interface is `eth0` (the first Ethernet card). Change `eth0` to the name of the external network interface of your system. For example, if it's the second Ethernet card, the interface is `eth1`. For a dial-up PPP connection, the interface is `ppp0`.

## Start BitTorrent transfers

To download using BitTorrent, you have to run the BitTorrent client. You use a URL to identify the `torrent`, which refers to the collection of files that you want to download. The URL also identifies the *tracker* — the server that hooks up your system's BitTorrent client with others that can provide parts of the files you want. In turn, the tracker also lets other clients begin requesting the torrent from your system.

Follow these steps to download one of the Fedora Core torrents:

- Visit the Fedora Core tracker at `torrent.dulug.duke.edu`.

You find a list of different torrent files listed at this site. Locate the file that you want. For example, if you are planning to burn Fedora Core CDs, you want the torrent for the Fedora Core binary ISO images.

- Open a terminal window and change to the directory where you want to store the files that you plan to download.
- Run the BitTorrent client.

Type the following command where *tfile* is the name of the torrent file that you want:

```
btdownloadcourses.py --url http://torrent.dulug.duke.edu/tfile
```

For example, to download the CD ISO images for Fedora Core 1 — provided in a torrent named *yarrow-binary-i386.iso.torrent* — you type:

```
btdownloadcourses.py --url http://torrent.dulug.duke.edu/yarrow-binary-i386.iso.torrent
```

The text screen (shown in Figure 5-1) shows you the status of the BitTorrent download as well as any uploads going on at the same time.

![](img/9f89727199836b0f871f1745838aa8b2_128_0.png)

**REMEMBER** If you install the BitTorrent software from a *tar.gz* file that you downloaded from *bitconjurer.org/BitTorrent/*, you have to change the directory to where the BitTorrent software is installed and then run the BitTorrent client with a command-line of the following form:

```
./btdownloadcourses.py --url torrentname
```

where *torrentname* is the URL of the torrent you want to access.

After BitTorrent finishes the download, leave the BitTorrent client running for as long as possible. This time enables your system to provide the file to others who are also joining BitTorrent. After all, this sharing is what makes BitTorrent such an efficient way to distribute files.

## Burning Fedora Core CDs

Linux distributions, including Fedora Core, are available for download from various Internet sites in the form of ISO images — an ISO image is an exact copy of an entire CD-ROM in a single, huge file (typically around 650MB). These files usually have the .iso extension. The ISO part of the name comes from the fact that the CD-ROM uses the ISO 9660 file system and image means the file is an exact replica of every bit of data on the CD-ROM.

In this project, I show you how to burn Fedora Core CDs from the ISO images by using the GnomeToaster application.

### Things you need

Here’s what you need to burn the Fedora Core CDs:

- A PC running Red Hat Linux or Fedora Core with the X-CD-Roast application installed (consult Book II, Chapter 4 for more information on how to install X-CD-Roast).
- An internal or external CD recorder.
- Blank CD-R media — you need four blanks for the four-CD Fedora Core.
- The downloaded Fedora Core ISO files. If you have not done so already, complete the BitTorrent project and download the four-CD Fedora Core ISO files.

### Steps to follow

Follow these steps to use X-CD-Roast to burn the Fedora Core CDs:

- Copy the Fedora Core ISO files to the directory specified in X-CD-Roast as the temporary image storage directory. For example, if you use /tmp as the image storage directory, copy the ISO files to the /tmp directory by using the cp or mv command.
- Choose Main Menu→System Tools→CD Writer from the GNOME or KDE desktop. If you aren’t logged in as root, you’re prompted for the root password. Then the X-CD-Roast main window appears.
- Click Create CD. X-CD-Roast displays the Create CD window.
- Click Write Tracks. X-CD-Roast displays two side-by-side panes: The right pane shows the names of the ISO image files, and the left pane shows what you want to burn on the CD. Initially, the left pane is empty.
- Select an ISO file on the right pane and click Add. X-CD-Roast shows the selected ISO file in the left pane as an item to be written to a CD-R.
- Click the Accept Track Layout button below the panes. X-CD-Roast changes the button to Write Tracks (and displays a few other buttons for performing other tasks).
- Insert a blank CD-R into the CD burner and click Write Tracks. X-CD-Roast then begins to burn the CD and shows the progress in a window. When the CD is done, X-CD-Roast ejects the CD.
- Repeat Steps 3 through 6 for the remaining Fedora Core ISO images.

## Preparing a Fedora Core DVD

Typically, the binary Fedora Core distribution takes four CDs and the source RPM files take another four CDs (there is also a rescue CD that lets you boot the system and fix problems). On the other hand, a DVD with its 4.7GB capacity can easily hold all the binary and source files for the complete Fedora Core distribution. (By the way, that’s why my publisher bundles a Fedora Core DVD with this book.)

![](img/9f89727199836b0f871f1745838aa8b2_130_0.png)

A word of caution about DVD capacity — when marketing people talk about the 4.7GB capacity of a DVD, they mean 4,700,000,000 bytes. However, for technology purists, that number translates to about 4,482MB or only 4.377GB because 1,024 bytes are in each KB and 1,024 x 1,024 = 1,048,576 bytes in a MB, and so on. The bottom line is that you can only fit about 4,482MB of data onto a DVD.

If you want to burn your own Fedora Core DVD, doing so is easy enough, provided you have a DVD recorder. This project guides you through the steps in burning a Fedora Core DVD.

### Things you need

Here’s what you need to burn the Fedora Core DVD:

- A PC running Red Hat Linux or Fedora Core. Note that you need Linux kernel version 2.4 or higher so that you can create a DVD ISO file that’s larger than 2GB.
- At least 10GB of available space on the hard drive (you need room for all the CD ISO files and the DVD ISO file you are about to create).
- An internal or external DVD recorder.
- Blank DVD recordable media in a format compatible with your DVD recorder — the media can be one of DVD-R, DVD-RW, DVD+R, or DVD+RW.
- The downloaded Fedora Core CD ISO files or, even better, the DVD ISO file. If you have not done so already, complete the BitTorrent project and download the four-CD Fedora Core ISO files or, if available, download the larger DVD ISO file.

### Steps to follow

The steps you follow to burn a Fedora Core DVD depend on whether you downloaded the Fedora Core CD ISO files or the DVD ISO file. If you download the CD ISO files, you have to first prepare a DVD ISO file from those CD images. After that, you can burn the DVD ISO file onto a DVD. I explain both steps.

If you have already downloaded the DVD ISO file, you can go right to burning the DVD.

### Create DVD ISO file from CD ISO files

Follow these steps to create a single DVD ISO file out of the four CD ISO files:

1. **Move the four ISO files to the /tmp directory using commands of the following form:**

   ```
   mv /full/path/ISOfilename.iso /tmp
   ```

   Replace the part /full/path/ISOfilename.iso with the full pathname of the ISO file. Repeat the copy command for all four CD ISO files.

2. **Create four directories that you can use as mount points for the four CD ISO images.**

   Assuming that you want these four directories in the /tmp directory, log in as root and type the following commands in a terminal window:

   ```
   cd /tmp
   mkdir ISO1
   mkdir ISO2
   mkdir ISO3
   mkdir ISO4
   ```

3. **Mount the four ISO files on the four mount points.**

   Assuming that the filenames for the four CD ISO image files are ISOfilename1.iso, ISOfilename2.iso, ISOfilename3.iso, and ISOfilename4.iso, type the following commands to mount them:

   ```
   mount -o ro,loop ISOfilename1.iso ISO1
   mount -o ro,loop ISOfilename2.iso ISO2
   mount -o ro,loop ISOfilename3.iso ISO3
   mount -o ro,loop ISOfilename4.iso ISO4
   ```

   Remember to replace the filenames with the actual filenames.
