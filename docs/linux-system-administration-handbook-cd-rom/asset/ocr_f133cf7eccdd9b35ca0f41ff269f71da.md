Some experimental modules available in the current 2.0 kernels include PCI bridge optimization, IP proxy support, IP multicast routing, ethernet bridging, frame relay support, Amiga FS support, and support for numerous pieces of less common hardware.

# Loadable Module Support

As you might guess, we highly recommend that you enable the use of loadable modules and kernel daemon support. The kernel daemon, kernel, is the program that manages the loading and unloading of modules. It is available separately from the kernel distribution.

# General Setup

You will definitely want to enable networking support, System V IPC, and support for ELF binaries. You should also enable a .out, probably as module since all newer Linux distributions are ELF-based. You should also compile the kernel in ELF format if you have a newer distribution.

If you plan on using the machine for Java development, enable Java binary support. It's fine to go with a module here unless you want to be able to run applets from the command line as well. If you do, you will need to compile the module into the kernel.

Set the processor type appropriately unless you have an old version of GCC for some reason. In that case you will have to say 386 or 486.

# Floppy, IDE, and Other Block Devices

Enable floppy disk support, probably as a module unless you use the floppy drive a lot. Leave out (E)IDE support if you are sure you don't need it (i.e., you have only SCSI hard drives and CD-ROMs).

The various chipset support and bug fixes can be left off unless you have an older motherboard, particularly one that uses Intel's Neptune chipset.

# Networking Options

The one option you will definitely want to enable here is TCP/IP networking. Enable it.