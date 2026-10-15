
course, you might get to the end of the 30 days and realize that Linux does what you want it to do and you don’t want to go back to Windows. Don’t be afraid; take the plunge!

## Relevant Ubuntu Commands

The following commands give you access to productivity applications, tools, and processes in Ubuntu:

- oowriter—OpenOffice.org's Writer
- oocalc—OpenOffice.org's Calc
- oompress—OpenOffice.org's Impress
- koshell—KDE's KOffice office suite shell
- kspread—KDE's KSpread spreadsheet
- gimp—The GIMP (GNU Image Manipulation Package)
- gnumeric—A spreadsheet editor for GNOME
- planner—A project management client for GNOME
- abiword—A graphical word processor for GNOME

## Reference

http://www.openoffice.org—The home page for the OpenOffice.org office suite.

http://www.pclinuxonline.com/modules.php?name=News&file=article&sid=3199—A set of links to tips, tricks, and enhancements for OpenOffice.org. One link at the site is to a PDF file that explains how to use OpenOffice.org as a database front end for MySQL.

http://www.gnome.org/projects/ooo/—The GNOME Office site.

http://www.koffice.org—The home page for the KOffice suite.

http://en.hancom.com/—The home page for the Hancom Office suite.

http://sourceforge.net/projects/ooextras/—This site provides templates, macros, and clip art, which are not provided with OpenOffice.org.

http://bulldog.tzo.org/webcal/webcal.html—The home page of the excellent WebCal web-based calendar and scheduling program.

http://www.codeweavers.com—Website of the hugely popular CrossOver Office from CodeWeavers that allows you to run Windows programs under Linux.

## CHAPTER 10

## Multimedia Applications

### IN THIS CHAPTER

- Burning CDs and DVDs in Ubuntu
- Sound and Music
- Viewing TV and Video
- Reference

Go up to anyone in the street today and ask them what an iPod is, and you are sure to get a correct answer. Apple's phenomenal success with their now ubiquitous personal music player has driven the digital music market like no one else. Rewind back to the early nineties then, where most users were limited to Windows' Sound Recorder and the idea of “ripping” CDs was virtually unheard of. Thankfully Linux has been at the forefront of the digital music landscape, although the continuing DRM saga can make it difficult to listen and manipulate digital media on the Linux platform.

Ubuntu itself is armed with a wide variety of applications designed to help you manage your digital media collection. You can rip music from CDs, stream them across your network, sync them with your personal music player, burn them to disc—in short you can do anything with them that you want.

This chapter takes you through the steps to burn CDs and DVDs using the tools supplied with Ubuntu. You will also find out how to rip music from CDs using a variety of tools, as well as the applications that can manage your music library. Finally we will take a look at how you can watch TV and video using Ubuntu.

> **NOTE**
> 
> Ubuntu is founded on the freedom of software, both in terms of free speech and free beer (see http://en.wikipedia.org/wiki/Free_Software for an explanation of the two terms) which means that it does not ship with any legally dubious software. By legally dubious, we mean any software that may infringe patents or other country-specific laws. One of the main casualties of

this is MP3 support which is the most widely used audio codec across the world. Of course we would recommend that you use the totally free and open source Ogg/Vorbis codec, but we also realize that you may already have splashed out on that new iPod and want to use it with Ubuntu. Fortunately, Ubuntu now comes with a handy tool called codecbuddy. Essentially, whenever you try to access a media file that uses a codec that Ubuntu doesn't currently have, codecbuddy attempts to find and install the necessary codec. It's very easy to use and should prevent you from having to trawl the Internet looking for codecs.

This will give you access to the LAME libraries, which will allow you to create MP3 files using Ubuntu.

Please make sure that you work within the laws of your country. We cannot be held responsible for you breaking the law!

## Burning CDs and DVDs in Ubuntu

Linux in general is distributed across the Internet by using ISOs that are waiting to be written to CDs or DVDs. Therefore learning how to burn discs is pretty essential if you have to download and install a Linux distribution. Not only that, but you will want to use CDs and, more commonly, DVDs to back up your music, family pictures, or other important files. With DVD writers being so cheap, the format has really taken off and more and more people use cheap DVDs as a way of archiving simply due to the larger storage size available. Today's high-resolution digital cameras can occupy upwards of 3MB per shot, and music files can be anything from 1MB to 10MB+ in size. These file sizes make DVD the obvious choice, but there are still occasions when you will need to write to a CD. You can use CDs and DVDs to

- Record and store multimedia data, such as backup files, graphics images, and music, on to a CD or DVD
- Rip audio tracks from a music CD (ripping refers to extracting music tracks from a music CD) and compile your own music CD for your personal use.

Linux audio clients and programs support the creation and use of many different types of audio formats. Later sections of this chapter discuss sound formats, sound cards, music players, and much more. Because CD burning is used for many other purposes in Ubuntu, we cover the essentials of that process first in this chapter. To record multimedia data on a CD, you must have installed a drive with CD writing capabilities on your system. Chapter 4, "Post-Installation Configuration," explains the rudiments of getting a CD writer configured and working properly. The hardware should have been set up properly during the initial Ubuntu installation. To make certain that your CD writer is working, use `cdrecord -scanbus` to get the information for using the CD drive under SCSI (small computer system interface) emulation:
