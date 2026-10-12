
## Old CD-ROM Drivers (Not SCSI or IDE)

Old CD-ROM drivers include the early SoundBlaster Matsumura and Panasonic CD-ROMs included on many 16-bit sound cards. If you have a clone card with a socket for a CD-ROM drive, and it was made before 1994, it is likely one of these interfaces; if it is newer, it could still be an IDE-type CD-ROM.

## Character Devices

Character devices communicate with the kernel via a stream of characters. These include terminals, serial ports, printers, cameras, voice synthesizers, and also some virtual devices such as the CMOS memory and the watchdog. If you’re working with most desktop installations, this section option will be simply a matter of adding or removing printer support. On the other hand, you’ll find this option very interesting if you’re working with data acquisition projects.

## Terminals and Consoles

Most applications will configure the kernel for at least one console. There are some embedded applications where this code will not be needed, but for most people, having multiple virtual consoles mapped to the Alt+Fn keys is very useful.

Another useful feature is to have console messages sent to a terminal attached to a serial device. This can be used to keep a printed log of system messages or have an emergency terminal port available on an otherwise head-less embedded application. Keep in mind that the serial console will not be enabled by default if you have a VGA card installed, and it must be explicitly enabled using the `console=ttyN` bootparam.

## Serial Ports

In addition to plain old serial ports, Linux also permits IRQ sharing (where supported by the hardware) and systems with more than four serial ports. Many data-acquisition systems and smaller ISPs also use the multiport serial boards that can be included with these options.

## Unix98 PTY

Linux now supports the Unix98 standard for the `/dev/pts` ports. This option requires glib-2.1 and also requires the `/dev/pts` filesystem, but it is highly recommended. Although it will take you some time to shift habits to the new naming convention, Linux has a clear resolve to move toward this system and obsolesce the old `/dev/tty` conventions. Under the new rules, pseudo-terminals are created on-the-fly under `/dev/pts/N`. The old convention of `/dev/tty` will become `/dev/pts/2` under the Unix98 system.

## Parallel Printer

You need this option to add a parallel-port printer, but keep in mind that this module supports the printer, not the port. You will also need to install and configure the parallel port (parport) module. Also, by default, the lp.o module will install itself on all available ports unless specified by bootparams.

## I²C Support

This option adds support for the alternate devices on Matrox graphics cards; this is a feature that lets you add multiple independent monitors to the same console.

## Mice

These options are for bus mice and PS/2-style mouse connectors, as found in some lap-top computers. Note that although some laptops do support PS/2-style mice (such as the ThinkPad 560), the internal pointer may still be a plain COM1-based serial mouse.

## Watchdog, NVRAM, and RTC Devices

The watchdog timer enables a character device (`mknod c /dev/watchdog 10 130`) used to reboot a locked machine. This feature is most often used with a watchdog daemon that will write to this device within the time limit. Linux includes support for a software watchdog and also for watchdog boards, which are not only more reliable, but several of them can also monitor the temperature inside your machine and force a shut-down/reboot when this rises above the allowed range.

The `/dev/nvram` option enables a new character device (`mknod c /dev/nvram 10 144`) for read/write access to the 50-byte CMOS memory.

All computers have a real-time clock; Linux lets you use it. This option will support a new character device (`mknod c /dev/rtc 10 135`) to generate reliable signals from 2Hz to 8kHz. The clock can also be programmed as a 24-hour alarm to raise IRQ8 when the alarm goes off. The rtc module is controlled by synchronized ioctl calls and is most often used for high-frequency data acquisition where you don’t want to burn up CPU cycles polling through the time-of-day calls. Example code for using the rtc module can be found in `Documentation/rtc.txt`.

## DoubleTalk Speech Synthesizer

No surprises here, however users of speech synthesizers may also be interested in the Blindlinux (distribution for the blind) and Emacspeak. Linux stands alone as the one OS that grants blind users total access to all functions of their computers and full access to all services on the Internet.

## Video for Linux (V4L)

Video4Linux (V4L) is a common programming API for audio/video capture or overlay cards, radio tuning sources, teletext, and other TV-related VBI data. V4L support is needed if you plan to use any of the current TV/FM cards, and V4L can be used for videoconferencing cameras such as the Connectix Qcam. To use these services, you will also need v4L-aware applications. A few applications are currently archived at the V4L Archives (ftp://ftp.uk.linux.org/pub/linux/video4linux), and a few more, including capture and Webcam applications, are listed at the Room Three Web site (http://roomrunner.swansea.linux.org.uk/v4l.shtml).

## Joystick Support

Linux will now support digital, serial, and some USB joystick controllers. The developers also hope to include support for force-feedback joysticks. A current list of supported devices and applications can be found at the Linux Joystick Web page (http://atrey.karlin.mff.cuni.cz/vojtech/joysticks/).

## Ftape, the Floppy Tape Device Driver

This option is for tape drives that are connected to your existing floppy drive controller or that include their own high-performance FDC. With the widespread availability of cheap CD-writers, tape backup systems are becoming rare beasts, but still have a niche use.

## Filesystems

Linux is the only operating system to offer a common ground for heterogeneous computer networks. During your first Linux install, one of your tasks was to select from a long list of supported filesystems for your Linux partition. This tradition continues with the kernel filesystem and network filesystem support. When all of this is combined with the capability to launch arbitrary executables transparently through an emulator (see the section “Support for Misc Binaries”), the degree of inter-OS integration in Linux becomes very clear.

The Filesystems dialog itself has few surprises. If you need floppy disks, CD-ROMs, ZIP drives, or hard drive partitions in any of the supported filesystems, you can include it in the core kernel, or, preferably, build it as a module. The `/proc` and `/dev/pts` filesystems are highly recommended unless the kernel is being built for a specialized embedded application; without these features, many standard utilities will not work.

### MS-DOS and VFAT (Windows) Filesystems

The MS-DOS and VFAT filesystems are worth some special consideration, if only because they are so ubiquitous. The current kernel support for the MS-DOS/VFAT disks used by DOS, Windows, Windows 95, and Windows NT will only read and write to uncompressed disks and cannot be used on DoubleSpaced disks or partitions. To access DoubleSpaced drives, you will need to use the DOSEMU emulator, or try the dmsdosfs tools (`ftp://metalab.unc.edu/pub/Linux/system/filesystems/dosfs/`).

MS-DOS support is not needed if you only plan to access MS-DOS disks through the mtools programs (mdir, mcopy, and so on). MS-DOS support is needed only if you plan to run Linux on a second partition or hard drive and need access to files on the MS-DOS side, or if you want to mount ZIP drives or other shared media to move files between Linux and MS-DOS.

VFAT adds the additional support for long filenames and also provides several options for the DOS codepage and National Language Support for the default behavior in coping with the DOS 11-character filename limit. Details of these translation options can be found in `Documentation/filesystems/vfat.txt`.

### ISO 9660, UDF, and DVD Support

UDF is the new standard CD-ROM format and is intended to replace ISO9660. At this point in time, UDF support means Digital Video Disk (DVD) support. Although the kernel supports the conventional ISO 9660-format CD-ROMs and will also support the Microsoft Joliet extensions for Unicode filesystems, it does not yet offer UDF. A driver for DVD and other UDF peripherals is available through the TryLinux UDF project (`http://www.trylinux.com/projects/udf/`).

### Native Language Support

This section is a bit of a misnomer. These options do support different cultural languages, but they only support reading and displaying these character sets on Microsoft filesystems.

The first section option lists Microsoft codepages and is only an issue if your system needs to read filenames from an MS-DOS or Windows filesystem. Note that codepage support applies to filenames only, and not to the contents of the file. Similarly, to display characters from Microsoft VFAT or Joliet CD-ROM filesystems, you will also need to include at least one of the NLS options. You may select any number of languages for both systems, and any of these can be built as a module to be loaded only when needed.

### Network Filesystems

Network filesystems allow you to share disk resources. Although there are obvious applications for this on a large network, even those in a small office/home office setting may want to distribute their resources. For example, our office uses an old salvaged 486/33 machine as a multiuser X-terminal for the smoking lounge. This machine runs Linux 2.2.7 from a 60MB hard drive. 60MB is enough to get the system up and running, and from there, NFS is used to supply software directories and user disk resources from upstairs in the lab.
