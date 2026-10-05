
## Configuring the Kernel

To the right of each button is a help button that gives a small amount of information on the driver and some hints to help you decide if you want to enable it or not.

If you are in X, run "make xconfig" from /usr/src/linux. If you are using a character terminal, run "make menuconfig". If you are using a character terminal with poor emulation, you are stuck running "make config."

When you make with the xconfig option, a nice GUI pops up as seen in Figure 18-1.

![](img/cd7585e53abd949068548271c07fcdd8_285_0.png)

Figure 18–1 Kernel X-based configuration tool.

## 8.6 Dive On In!

Once you go into a submenu, you can get help on the various options there. See Figures 18-2 and 18-3 for examples.

![](img/cd7585e53abd949068548271c07fcdd8_286_0.png)

Figure 18–2 Submenu pop-up.

![](img/cd7585e53abd949068548271c07fcdd8_286_1.png)

Figure 18–3 Submenu help pop-up.

Kernel modules are small pieces of compiled code which can be inserted or removed from the running kernel, using the programs insmod and rmmod. This is described in the file Documentation/modules.txt. Modules can be device drivers, file systems, binary executable formats, and so on. If you think that you may want to make use of modules with this kernel in the future, then say Y. If unsure, say Y.

Now, you are ready to start configuring your new kernel.

### Maturity Options

Answering yes to the one option here will not change the kernel. It will simply give you options later on for various experimental or incomplete drivers. Say yes. It doesn't hurt anything. You can always say no to any experimental drivers you are offered. 

Some experimental modules available in the current 2.0 kernels include PCI bridge optimization, IP proxy support, IP multicast routing, ethernet bridging, frame relay support, Amiga FS support, and support for numerous pieces of less common hardware.

### Loadable Module Support

As you might guess, we highly recommend that you enable the use of loadable modules and kernel daemon support. The kernel daemon, kernel, is the program that manages the loading and unloading of modules. It is available separately from the kernel distribution.

### General Setup

You will definitely want to enable networking support, System V IPC, and support for ELF binaries. You should also enable a .out, probably as module since all newer Linux distributions are ELF-based. You should also compile the kernel in ELF format if you have a newer distribution.

If you plan on using the machine for Java development, enable Java binary support. It's fine to go with a module here unless you want to be able to run applets from the command line as well. If you do, you will need to compile the module into the kernel.

Set the processor type appropriately unless you have an old version of GCC for some reason. In that case you will have to say 386 or 486.

### Floppy, IDE, and Other Block Devices

Enable floppy disk support, probably as a module unless you use the floppy drive a lot. Leave out (E)IDE support if you are sure you don't need it (i.e., you have only SCSI hard drives and CD-ROMs).

The various chipset support and bug fixes can be left off unless you have an older motherboard, particularly one that uses Intel's Neptune chipset.

### Networking Options

The one option you will definitely want to enable here is TCP/IP networking. Enable it.

## 18.6 Dive On In!

Most of the rest of the IP and network-related options you will not need unless your machine is acting as a TCP/IP router/gateway. You might need to enable multicasting if you are going to be accessing the MBONE (the Multicast Backbone which sits on top of the Internet).

Further down you will find the support for other networking protocols: IPX, AppleTalk, and AX.25. Enable these as you need them. If your machine is going to be a server using one of these protocols, you might as well compile in the kernel. It will likely end up being loaded nearly all of them anytime.

### SCSI Support

Assuming we have beaten the dead horse enough, you will need at least SCSI support and SCSI disk support. Probably you will need SCSI tape and CD-ROM support as well. If you have other SCSI devices, like a scanner, you will also need to enable generic SCSI support. Unless you have a device with logical unit numbers, you should say no to the option for probing all logical unit numbers (LUNs). An example of such a device is a CD jukebox.

If you are having problems with your SCSI bus, you may want to enable verbose error reporting to help track the errors.

### SCSI Low-Level Drivers

Enable the driver(s) for your SCSI adapters. If you are using a Zip or Jaz drive that came with it, you will need to enable its driver. See the chapter on peripherals for more information.

If you are using a zip drive on the parallel port, you will need to enable support for it here. This type of drive contains a parallel-to-SCSI converter that essentially turns the port into a SCSI host.

### Network Device Support

Enable network device support (duh). After that, enable other options as you need. This is the only situation where you will want this enabled.

### ISDN Subsystem

Enable this if you need it. You will need the manual for your sound card as there are a number of hardware parameters you need to compile the kernel.

### CD-ROM Drivers (ATAPI)

If your CD-ROM is attached to the IDE, you will want to enable support for it. You will need the manual for your sound card as there are a number of hardware parameters you need to compile the kernel.

### Filesystems

If you have a very heterogeneous LAN, you may want to enable all of these for removable media (floppy, Jaz drives).
