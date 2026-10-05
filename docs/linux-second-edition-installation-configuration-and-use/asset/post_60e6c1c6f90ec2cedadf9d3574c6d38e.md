
## 206 CONFIGURATION AND ADMINISTRATION

| Code maturity level options | Taking devices | Network File Systems |
|---|---|--|
| Processor type and features | Wan interfaces | Partition Types |
| Loadable module support | Amateur Radio support | Native Language Support |
| General setup | | General setup |
| Plug and Play support | | |
| Block devices | ISDN subsystem | y n Networking support Help |
| Networking options | CD-ROM drivers | y n Help |
| | Character devices | y n PCI access mode Help |
| SCSI support | Any | y n PCI quirks Help |
| SCSI low level drivers | Mice | y n Help |
| Network device support | | Video For Linux Help |
| ARConnect devices | Joystick support | y n Backward-compatible |
| Ethernet (10 or 100mbit) | Flope, the floppy | y n WCA support Help |
| Applet devices | Filesystems | y n System IPC Help |
| | | Main Menu Next Prev |

Figure 6.2 Kernel configuration under X.

Doubt, please read the very informative help texts available for each option. However, if you have little experience with Linux or any other Unix, this information will confuse you. Therefore, this section presents further basic information on this subject without, however, dealing in depth with every single option.

## Fundamentals

Basically, you have to decide between two types of kernel: monolithic kernels contain all required drivers directly in the kernel and do not support modules. Modularized kernels are capable of including additional modules on top of the integrated kernels during current operation. As a rule, a modularized kernel is the better option. For many components, you have the choice between three alternatives: YES / MODULE / NO. YES means that this component is directly integrated into the kernel. MODULE means that this component is compiled as a modularized kernel, NO means that the component is not compiled at all. With a monolithic kernel, you must specify NO for all components that you do not require (otherwise the kernel becomes unnecessarily large). With a modularized kernel, NO will save you some time (because the module does not have to be compiled), but you lose flexibility. Who knows whether you will not need this module at some point in the future?

## RECOMPILING THE KERNEL 207

CAUTION: No matter whether you are building a monolithic or a modularized kernel: you must in any case integrate directly (option YES) all components that you need for booting. If, for example, the root partition is located on a SCSI disk, the corresponding SCSI driver must not be a module, but an integrated part of the kernel. If the root partition is an ext2 file system (presumably on 99 cent of all Linux computers), this module needs to be integrated into the kernel.

## Options after options ...

### Code maturity level
Here you can specify whether the Alpha driver and other half-finished components should be considered for the configuration. Normally, you will do without them. You need to specify YES only if you want to test new kernel components.

### Processor type
The processor selection (386, 486, Pentium, or Pentium Pro) influences speed and size of the code. Please note that the code is upward compatible, but not downward compatible. Compatible code can therefore be executed on any Pentium without problems, whereas Pentium Pro might cause a crash on a traditional Pentium. Math emulation is only if you have a very old processor without a coprocessor (such as 386, 486, SX). If you have a motherboard with only one CPU (which is usually the case), you must use the Symmetric multi-processing option to NO.

### General setup
System IPC is a further form of Linux internal communication used by several programs (especially the DOS emulator) – therefore you should say YES to this option as well.
New distributions exclusively consist of ELF programs. Then, you definitely need ELF support. Often, older programs must be executed in the out binary format – therefore you should select YES or MODULE for this option as well.
The Parallel port support refers to the parallel interface to which the printer is usually connected: YES or MODULE.

## CONFIGURATION AND ADMINISTRATION

### Plug and play support
Here you can activate the (still rudimentary) support for plug & play cards. Do not expect that thanks to this de-activates to this option the kernel will fully recognize every plug & play hardware device – as a rule, you will still need the isapnp utility program.

### Block devices
Floppy support is probably a matter of course. Also with Enhanced IDE support the correct support is probably a matter of course. Also with Enhanced IDE support the correct setting is nearly always EIDE (not MODULE), EIDE hard disks must already work during booting! Some additional options concern EIDE special devices and bugfixes. (Some EIDE cards are faulty and the kernel contains special code that circumvents these faults).

Use DMA by default activates bus master DMA mode, if the motherboard and hard disk are recognized. If this is not the case, the hardware command must be used to activate this performance-increasing mode manually (see page 156). In rare cases, automatic DMA activation leads to problems – in this case you need to specify No-ROMs. This is not the loopback interface normally only if you plan to burn CD-loopback interface from network configuration, but the flexibility of using as a file system. When this component is available, you can mount and check an ISO as a read-only file system (using mounting).
Multiple devices support all several hard disk partitions to be combined into one logical partition (RAID, see also page 157).
Some distributions (in particular RedHat) have a RAM disk for loading modules (usually a SCSI driver), this detour is omitted. However, in case you wish to use a RAM disk for booting, you must specify the relevant modules.

Network options
Here, our advice is that, in case of doubt, read the very informative help texts available for each option. However, if you have little experience with Linux or any other Unix, this information will confuse you. Therefore, this section presents further basic information on this subject without, however, dealing in depth with every single option.

SCSI support
If you use a SCSI disk, you must answer YES to the first two options; for a SCSI disk, to the next two options as well.

Network device support
If you want to communicate with another computer in any form whatsoever, this is the place to select YES. Also if your computer is only to be connected to the Internet via PPP/SLIP. Dummy support is often needed for SLIP configuration. PLIP allows data exchange via the parallel port (a reasonable choice only in very rare cases); printer access is then no possible. PPP and SLIP are two variations to exchange access via the serial interface. If you do not know which Internet provider provides (probably PPP), simply select both.

XY network devices
You need to set the appropriate options to YES or MODULE, if you want a corresponding card. The popular NE-200-compatible cards belong to the subgroup Other ISA cards of the Ethernet (10 or 100 Mbits) group. The PCI version of this card can be found in the subgroup EISA, PCI and onboard controllers. Do not activate a network card that you do not have!

### ISDN support
If you want to use ISDN. Information about ISDN can also be found on the following WWW page:

```
http://alumni.caltech.edu/~dank/isdn/
http://www.suse.com (support database, keyword ISDN)
```

### CD-ROM drivers
In most cases you will not have to select any option, even if you possess a CD-ROM drive. Here, only CD-ROM drives are listed that have their own interface. Most of the common CD-ROM drives, however, are IDE (block devices) or SCSI drives (see SCSI support).

### Character devices
The options Virtual terminal and Support for console must be YES – otherwise you cannot ever log in locally.

Standard serial support and Parallel printer support are needed to use the serial and parallel interfaces. Mouse support refers to mice that are not connected to the
