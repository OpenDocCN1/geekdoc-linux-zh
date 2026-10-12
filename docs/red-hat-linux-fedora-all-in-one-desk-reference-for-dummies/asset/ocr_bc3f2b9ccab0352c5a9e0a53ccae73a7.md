plug-in, in the form of an RPM file — `xmms-mpg123-1.2.7-21.i386.rpm` — is available for `havardk.xmms.org/dist/xmms-1.2.7-rh8-rh9-rpm/` `xmms-mpg123-1.2.7-21.i386.rpm` (for other versions of Red Hat Linux, look in an appropriate directory in `havardk.xmms.org/dist/`). After downloading the RPM file, log in as `root` and type `rpm -ivh xmms-mpg123*` to install the plug-in. The next time you run XMMS, you can play MP3 files in XMMS. Easy, isn't it?

# Burning a CD

Red Hat Linux includes the GnomeToaster, a graphical CD burner application with a lot of features. It can create both data CDs and audio CDs. You can also *rip* (copy) music from audio CDs to files on the hard drive and then burn them onto a new audio CD. If you happen to download Red Hat Linux ISO images (a huge data file with the exact replica of a CD-ROM), you can use GnomeToaster to create a CD from that ISO image. In the next few sections, I briefly explain how to use GnomeToaster. If you want to learn more, visit `gnometoaster.rulez.org`.

![](bbox=[0.15, 0.55, 0.26, 0.68])

GnomeToaster depends on many external programs to do its job. If these external programs do not exist, then some GnomeToaster features won't work. Although most programs used by GnomeToaster come with Red Hat Linux, a few are not part of the Red Hat Linux distribution. For example, GnomeToaster needs the `mpg123` program to convert MP3 audio files into a form suitable for recording on CD. Red Hat Linux does not come with the `mpg123` program, so you can't create audio CDs that include MP3 songs.

Before you can burn a CD, you need a CD-R or CD-RW drive (CD burner) connected to your PC. It can be an internal or an external CD burner. Internal CD burners are usually IDE (also known as ATAPI) devices connected to the same card that supports the PC's hard drive and any other CD-ROM drive.

![](bbox=[0.15, 0.84, 0.26, 0.97])

If you have an external CD burner, it probably connects to your PC's USB port. When you connect such a burner to the USB port and power up the burner, Red Hat Linux should automatically recognize the device and load the appropriate USB driver. When you use GnomeToaster to burn a CD on a USB CD-R/RW drive, you do not have to do anything special — GnomeToaster automatically detects most CD-ROM and CD-R/RW drives on your system. You do, however, have to manually identify the ATAPI CD drives.

To start GnomeToaster, choose Main Menu→System Tools→More System Tools→CD Writer from the GNOME or KDE desktop. If you're not logged in as `root`, you're prompted for the `root` password. The GnomeToaster main window appears, as shown in Figure 5-8. You can do everything — configure GnomeToaster and burn audio and data CDs — from the main window.