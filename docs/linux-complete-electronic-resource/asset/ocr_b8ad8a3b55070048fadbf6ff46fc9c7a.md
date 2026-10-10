You also need an MDA, Hercules, CGA, EGA, VGA, or Super VGA video card and monitor. In general, if your video card and monitor work under MS-DOS, it should work under Linux. However, if you wish to run X-Windows, there are other restrictions on the supported video hardware. The Linux XFree86-HOWTO, http://MetaLab.unc.edu/LDP/HOWTO/XFree86-HOWTO.html, contains more information about running X and its requirements.

You’ll want a CD-ROM drive. If it’s ATAPI, SCSI, or true IDE you should have no problem making it work (but watch for cheap drives advertising “IDE” interfaces that aren’t true IDE). If your CD-ROM uses a proprietary interface card, it’s possible the installation kernel you’re going to boot from a floppy won’t be able to see it—and an inaccessible CD-ROM is an installation showstopper. Also, CD-ROMs that attach to your parallel port won’t work at all. If you’re in doubt, consult the Linux CD-ROM HOWTO, http://MetaLab.unc.edu/LDP/HOWTO/CDROM-HOWTO.html, for a list and details of supported hardware.

So-called Plug’n’Play jumperless cards can be a problem. Support for these is under active development but not there yet in the 2.0.25 kernel. Fortunately this is only likely to be a problem with sound or Ethernet cards.

If you’re running a box that uses one of the Motorola 68k processors (including pre-PowerPC Macintosh, Amiga, Atari, or VMEbus machines), see the Linux m68k FAQ at http://www.clark.net/pub/1awrencec/linux/faq/Faq.html for information on minimum requirements and the state of the port. The FAQ now says m68k Linux is as stable and usable as the Intel versions.

# Space Requirements and Coexistence

You’ll need free space for Linux on your hard drive. The amount of space needed depends on how much software you plan to install. Most installations require somewhere in the ballpark of 200 to 500 megs. This includes space for the software, swap space (used as virtual RAM on your machine), free space for users, and so on.

It’s conceivable that you could run a minimal Linux system in 80 megs or less (this used to be common when Linux distributions were smaller), and it’s conceivable that you could use well over 500 megs or more for all of your Linux software. The amount varies greatly depending on the amount of software you install and how much space you require. I’ll discuss this in more detail later.

Part I