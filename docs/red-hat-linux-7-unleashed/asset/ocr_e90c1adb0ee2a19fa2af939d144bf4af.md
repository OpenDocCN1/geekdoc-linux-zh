# Old CD-ROM Drivers (Not SCSI or IDE)

Old CD-ROM drivers include the early SoundBlaster Matsumita and Panasonic CD- ROMs included on many 16-bit sound cards. If you have a clone card with a socket for a CD-ROM drive, and it was made before 1994, it is likely one of these interfaces; if it is newer, it could still be an IDE-type CD-ROM.

# Character Devices

Character devices communicate with the kernel via a stream of characters. These include terminals, serial ports, printers, cameras, voice synthesizers, and also some virtual devices such as the CMOS memory and the watchdog. If you’re working with most desktop installations, this section option will be simply a matter of adding or removing printer support. On the other hand, you’ll find this option very interesting if you’re working with data acquisition projects.

# Terminals and Consols

Most applications will configure the kernel for at least one console. There are some embedded applications where this code will not be needed, but for most people, having multiple virtual consoles mapped to the Alt+Fn keys is very useful.

Another useful feature is to have console messages sent to a terminal attached to a serial device. This can be used to keep a printed log of system messages or have an emergency terminal port available on an otherwise head-less embedded application. Keep in mind that the serial console will not be enabled by default if you have a VGA card installed, and it must be explicitly enabled using the `console=ttyN` bootparam.

# Serial Ports

In addition to plain old serial ports, Linux also permits IRQ sharing (where supported by the hardware) and systems with more than four serial ports. Many data-acquisition systems and smaller ISPs also use the multiport serial boards that can be included with these options.

# Unix98 PTY

Linux now supports the Unix98 standard for the `/dev/pts` ports. This option requires glib-2.1 and also requires the `/dev/pts` filesystem, but it is highly recommended. Although it will take you some time to shift habits to the new naming convention, Linux has a clear resolve to move toward this system and obsolesce the old `/dev/tty` conventions. Under the new rules, pseudo-terminals are created on-the-fly under `/dev/pts/N`. The old convention of `/dev/tty` will become `/dev/pts/2` under the Unix98 system.