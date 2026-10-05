# Terminals and Consoles

Most applications will configure the kernel for at least one console. There are some embedded applications in which this code will not be needed, but for most people, having multiple virtual consoles mapped to the Alt+Fn keys is very useful.

Another useful feature is that you can have console messages sent to a terminal attached to a serial device. This can be used to keep a printed log of system messages or have an emergency terminal port available on otherwise console-less embedded application. Keep in mind that even if you select this option, the serial console will not be enabled by default if you have a VGA card installed, and it must be explicitly enabled using the console=ttyN kernel boot option.

# Serial Ports

In addition to plain old serial ports, Linux will permit IRQ sharing (where supported by your hardware) and systems with more than four serial ports. Many data-acquisition systems and smaller ISPs also use multiport serial boards, which can be included with the options.

# UNIX98 PTY

Linux 2.2 now supports the UNIX98 standard for the /dev/pts ports. This option requires glibc-2.1 and the /dev/pts filesystem, but it is highly recommended. Although it will take you time to get used to the new naming convention, Linux has a clear resolve to move towards this system and make the old /dev/tty connections obsolete. Under the new rules, pseudo-terminals are created on-the-fly under /dev/pts/N. The old convention of /dev/ttype2 will become /dev/pts/2 under the UNIX98 system.

# Parallel Printer

You will need this option if you plan to add a parallel-port printer, but keep in mind that this module supports the printer, not the port. You will also need to install and configure the parallel port (parport) module. Also, by default, the 1lp.o module will install itself on all available parallel modules unless specified in the boot command line, /etc/lilo.conf append line, or /sbin/ins/insmod command line.

# Mice

This option is for machines with bus mice and PS/2-style mouse connectors, as found in some laptop computers. Note that although some laptops support PS/2 style mice (such as the Thinkpad 560), the internal pointer may still be a plain COM1-based serial mouse.