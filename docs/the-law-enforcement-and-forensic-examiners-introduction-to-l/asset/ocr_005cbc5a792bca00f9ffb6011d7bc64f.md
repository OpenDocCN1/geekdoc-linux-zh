# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

First, let's make sure we can find lshw, and then read the README file:

```
root@forensic1:~#$ sbofind lshw
SBo: lshw
Path: /usr/sbo/repo/system/lshw
```

```
root@forensic1:~# sbofind -r lshw
SBo: lshw
Path: /usr/sbo/repo/system/lshw
```

README:
lshw (Hardware Lister) is a small tool to provide detailed detailed information on the hardware configuration of the machine. It can report exact memory configuration, firmware version, motherboard configuration, CPU version and speed, cache configuration, bus speed, etc. on DMI-capable x86 or EFI (IA-64) systems and on some PowerPC machines (PowerMac G4 is known to work).

Information can be output in plain text, XML, or HTML.

It currently supports DMI (x86 and EFI only), Openfirmware device tree (PowerPC only), PCI/AGP, ISA PnP (x86), CPUID (x86), IDE/ATA/ATAPI, PCMCIA (only tested on x86), USB, and SCSI.

On x86, lshw needs to be run as root to be able to access DMI information from the BIOS. Running lshw as a non-root user usually gives much less detailed information.

When we actually run the sboinstall command, the README is displayed by default anyway, but we want to make it explicit. I prefer to read the README before the install command so I know what to expect and what caveats to prepare for. And how we simply install the build:

```
root@forensic1:~# sboinstall lshw
...
Proceed with lshw? [y]
...
Install queue: lshw
Are you sure you wish to continue? [y]
...
Executing install script for lshw-B.02.18-x86_64-1_SBo.tgz.
Package lshw-B.02.18-x86_64-1_SBo.tgz installed.
```

Cleaning for lshw-B.02.18...