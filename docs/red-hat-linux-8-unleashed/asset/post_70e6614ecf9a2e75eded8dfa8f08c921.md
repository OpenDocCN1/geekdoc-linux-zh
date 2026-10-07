
# Using the cds.o File System Module

Not included with Red Hat is an interesting kernel module cds.o. This filesystem module lists every track and image on a CD as a separate file. This is a useful tool for recovering data from multibision CDs. Each session is listed as an image filesystem that can then be mounted using the loopback filesystem. (Refer to Chapters 10, "Managing the Filesystems," and 11, "Backing Up, Restoring, and Recovery," for examples of mounting image files in this way.) You can get cds.o from http://www.elis.rug.cz/~ronsese/cds/; you must compile it with your system using the ./configure, make and make install commands. Load it with `modprobe cds`, and mount a CD with `mount -t cds -o /dev/cdrom /mnt/cdrom`. Although the cdsfs module isn't the most elegant approach to CD filesystems, it's a handy tool for CD data recovery.

# Creating CDs from the Command Line

In Linux, creating a CD is a two-step process. You first create the iso9660-formatted image, and then you burn or write the image onto the CD. iso9660, as you learned in Chapter 10, is the default filesystem for CD-ROMs.

Use the mkisofs command to create the ISO image. The mkisofs has many options (see the main page for a full listing), but use the following for quick burns:

```
$ mkisofs -r -v -J -I /tmp/our_special_cd.iso /source_directory
```

The options used in this example are as follows:

- -r: Sets permission of the files to make more useful values. UID and GID (individual and group user requirements) are set to zero, all files are globally readable and searchable, and all files are set as executable (for Windows systems).
- -v: Displays verbose messages (rather than terse messages) so you can see what is occurring during the process; these help resolve problems if they occur.
- -J: Uses the Juliet extension to ISO 9660 so your Windows-building candies can read the CD. Juliet (for Windows), Rock Ridge (for Unix), and HSF (for Mac) for the iso9660 standard are used to accommodate long filenames rather than the eight-character DOS filenames that the iso9660 standard supports.
- -I: A lowercase L allows 31 character filenames; DOS doesn't like it, but everyone does.
- -o: Sets the directory where the image will be written (that is, the output). The /tmp directory is convenient for this purpose, but the image could go anywhere you write permissions.
- -R: Indicates the path to the source directory; that is, the directory that contains the files we want to include. There are ways to append additional paths and exclude directories (and files) under the specified path—it's explained in the main page if you need that level of complexity. Our simple solution is to construct a new directory tree and populate it with the files we want to copy, then make the image using that directory as the source.

Many more options are available, including options to make the CD bootable.

After you've created the ISO image, you can write it to the CD with the cdrecord command:

```
$ cdrecord -eject -v speed=12 dev=0,0 /tmp/our_special_cd.iso
```

The options used in this example are as follows:

- -eject: Ejects the CD when the write operation is finished.
- -v: Displays verbose messages.
- speed: Sets the speed; the rate depends on the individual drive's capabilities. If the drive or the recordable medium is poor, you can use lower speeds to get a good burn.
- dev: Specifies the number of the CD writer (the number I told you to write down earlier).

> NOTE
> You can use the blank option with the cdrecord command to erase CD-RW disks. The cdrecord command has fewer options than mkisofs, but it also has the -multi option, which enables you to use multisision CDs. A multisision CD enables you to write a data track, and then add more data to the CD later. A single CD can be written to only once; any leftover CD capacity is wasted. Read about other options in the cdrecord page.

Current capacity for CD media is 700MB of 80 minutes of music. Some CDs can be overburned, that is, recorded to a capacity in excess of the standard. The cdrecord command is capable of overflowing if your CD-RW drive supports it. You can learn more about overflowing CDs at http://www.gamecopyworld.com/.

# Creating CDs with Red Linux Graphical Clients

Although adequate for quick burns and in shell scripting, the command line technique for burning CDs is an awkward choice for many people, until they become proficient and it will learn all the commands. Red Hat provides several graphical clients. The following sections describe KDE's KOnCD, as well as a number of other graphical clients for burning audio and data CDs.

> TIP
> A excellent Internet site for CD-related information is http://www.gamecopyworld.com/. It offers in-depth discussion of technical data concerning CD media and CD records. Additional CD-related applications can be found through a search at Freshmeat.net.

Also, the Gracenote DB Music Recognition Service licenses a database to software developers so they can include additional functionality in their application by accessing the database and having their application display information about the music CD, including the artist and song title, the CD's track list, and so on. The database server at cddb.cddb.org will, when contacted by the appropriate software, identify the CD and send the information locally. Many CD-related applications provide this functionality.

Each GUI for burning CDs has different strengths and weaknesses. You should experiment with all the different tools as well as try the command-line.

# Using KOnCD

KOnCD is a graphical client that you can use to copy a CD, make a data CD, make an audio CD, or erase a CD-RW. The setup of KOnCD is straightforward, as shown in Figure 26.1. An useful feature of KOnCD is the capability to add users to the group allowed to use the CD writer. KOnCD will automatically detect many, if not all, of the appropriate defaults.

After you've added the client's users, you can set up the image options (as you did with the options you added to mkisofs command). The Image Type drop-down list displays the collection of predefined options (see Figure 26.2). You can choose advanced image options in the upper area of the window. Check an option to enable it; check the check box to turn the option off. When you've finished choosing options, click the Save button.

# CHAPTER 26 Multimedia Applications

Ripping audio tracks from a CD is handled by the interface shown in Figure 26.3. If you click on the RC button from the menu list, you can select the format of the output music file from a drop-down list. The formats for the output tracks include Raw, Ogg-Vorbis, Wave, and MP3; don't choose MP3, because doing so causes an error. (See the “Sound Formats” section in this chapter for a full explanation of these formats and the issues surrounding MP3.)
