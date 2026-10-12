
## D.9 Alpha Architecture Notes

32-bit and 64-bit loads and stores (longword and quadword, in Digital’s nomenclature). The co-architects (Dick Sites, Rich Witek) justified this decision by citing the advantages:

- Byte support in the cache and memory sub-system tends to slow down accesses for 32-bit and 64-bit quantities.
- Byte support makes it hard to build high-speed error-correction circuitry into the cache/memory sub-system.

Alpha compensates by providing powerful instructions for manipulating bytes and byte groups within 64-bit registers. Standard benchmarks for string operations (e.g., some of the Byte benchmarks) show that Alpha performs very well on byte manipulation.

The absence of byte loads and stores impacts some software semaphores and impacts the design of I/O sub-systems. Digital’s solution to the I/O problem is to use some low-order address lines to specify the data size during I/O transfers, and to decode these as byte enables. This so-called Sparse Addressing wastes address space and has the consequence that I/O space is non-contiguous (more on the intricacies of Sparse Addressing when I get around to writing it). Note that I/O space, in this context, refers to all system resources present on the PCI and therefore includes both PCI memory space and PCI I/O space.

With the 21164A introduction, the Alpha architecture was ECo’d to include byte addressing. Executing these new instructions on an earlier CPU will cause an OPCDEC PALCode exception, so that the PALCode will handle the access. This will have a performance impact. The ramifications of this are that use of these new instructions (IMO) should be restricted to device drivers rather than applications code.

These new byte load and stores mean that future support chipsets will be able to support contiguous I/O space.

### D.9 PALCode and all that stuff

This is a placeholder for a section explaining PALCode. I will write it if there is sufficient interest.

## D.10 Porting

The ability of any Alpha-based machine to run Linux is really only limited by your ability to get information on the gory details of its innards. Since there are Linux ports for the E66, EB64+ and EB164 boards, all systems based on the 21066, 21064/APECS or 21164/ALCOR should run Linux with little or no modification. The major thing that is different between any of these motherboards is the way that they route interrupts. There are three sources of interrupts:

- On-board devices
- PCI devices
- ISA devices

All the systems use an Intel System I/O bridge (SIO) to act as a bridge between PCI and ISA (the main I/O bus is PCI, the ISA bus is a secondary bus used to support slow-speed and 'legacy' I/O devices). The SIO contains the traditional pair of daisy-chained 8259s.

Some systems (e.g., the Noname) route all of their interrupts through the SIO and thence to the CPU. Some systems have a separate interrupt controller and route all PCI interrupts plus the SIO interrupt (8259 output) through that, and all ISA interrupts through the SIO.

Other differences between the systems include:

- How many slots they have
- What on-board PCI devices they have
- Whether they have Flash or EPROM

## D.11 More Information

All of the DS evaluation boards and motherboard designs are license-free and the whole documentation kit for a design costs about $50. That includes all the schematics, programmable parts sources, data sheets for CPU and support chipset. The doc kits are available from Digital Semiconductor distributors. I’m not suggesting that many people will want to rush out and buy this, but I do want to point out that the information is available.

Hope that was helpful. Comments/updates/suggestions for expansion to Neal Crook, neal.crook@reo.mts.digital.com

## D.12 References

http://www.research.digital.com/wrl/publications/abstracts/TN-13.html
Bill Hamburgen, Jeff Mogul, Brian Reid, Alan Eustace, Richard Swan, Mary Jo Doherty, and Joel Bartlett. Characterization of Organic Illumination Systems. DEC WRL, Technical Note 13, April 1989.

# Appendix E

# Alpha Miniloader Howto

This document describes the Miniloader, a program for Alpha based systems that can be used to initialize the machine and load Linux. The Alpha Linux Miniloader (to give it it's full name) is also known as Milo.

## E.1 Introduction

This document describes the Miniloader for Linux on Alpha AXP (Milo). This firmware is used to initialize Alpha AXP based systems, load and start Linux and, finally, provide PALCode for Linux.

### E.1.1 Copyright

The Alpha Miniloader (Milo) HOWTO is Copyright ©1995, 1996 David A Rusing.

> **Copyright** Like all Linux HOWTO documents, it may be reproduced and distributed in whole or in part, in any medium, physical or electronic, so long as this copyright notice is retained on all copies. Commercial redistribution is allowed and encouraged; however the author would *like* to be notified of such distributions. You may translate this HOWTO into any language whatsoever provided that *you leave this copyright statement and*

disclaimer intact, and that you append a notice stating who translated the document.

**Disclaimer** While I have tried to include the most correct and up to date information available to me, I cannot guarantee that usage of information in this document does not result in loss of data or equipment. I provide NO WARRANTY about the information in the HOWTO and I cannot be made liable for any consequences resulting from using the information in this HOWTO.

### E.1.2 New Versions of this Document

The latest version of this document can be found in `ftp://gatekeeper.dec.com/pub/` and David Mosberger-Tang is kind enough to include the html form of it in his excellent Linux Alpha FAQ site `http://www.azstarnet.com/~explinux`.

## E.2 What is Milo?

On Intel based PC systems, the BIOS firmware sets up the system and then loads the image to be run from the boot block of a DOS file system. This is more or less what Milo does on an Alpha based system, however there are several interesting differences between BIOS firmware and Milo, not least of which is that Milo includes and uses standard Linux device drivers unmodified. Milo is firmware, unlike LILo, which relies on the BIOS firmware to get itself loaded. The main functional parts of Milo are:

1. PALCode,
2. Memory set up code (builds page tables and turns on virtual addressing),
3. Video code (BIOS emulation code and TGA (21030)),
4. Linux kernel code. This includes real Linux kernel code (for example, the interrupt handling) and ersatz or mock Linux kernel,
5. Linux block device drivers (for example, the floppy driver),
6. File system support (ext2, MS-DOS and ISO9660),
7. User interface code (MILO),
8. Kernel interface code (sets up the HWRPB and memory map for linux),
9. NVRAM code for managing environment variables.

The following paragraphs describe these functional parts in more detail.

PALCode can be thought of as a tiny software layer that tailors the chip to a particular operating system. It runs in a special mode (PALmode) which has certain restrictions but it uses the standard Alpha instruction set with just five extra instructions. In this way, the Alpha chip can run such diverse operating systems as Windows NT, OpenVMS, Digital Unix and, of course, Linux. The PALCode that Milo uses (and therefore Linux itself) is, like the rest of Milo, freeware. It is derived from Digital's Evaluation Board software example Digital Unix PALCode. The differences between the different PALCodes are because of differences in address mapping and interrupt handling that exist between the Alpha chips (21066 based systems have a different I/O map to 21064+2107x systems) and different Alpha based systems.

For Milo to operate properly it needs to know what memory is available, where Linux will eventually be running from and it must be able to allocate temporary memory for the Linux device drivers. The code maintains a memory map that has entries for permanent and temporary allocated pages. As it boots, Milo decompresses itself into the correct place in physical memory. When it passes control to the Linux kernel, it reserves memory for the compressed version of itself, the PALCode (which the kernel needs) and some data structures. This leaves most of the memory in the system for Linux itself.

The final act of the memory code is to set up and turn on virtual addressing so that the data structures that Linux expects to see are at the correct place in virtual memory.

Milo contains video code that initialises and uses the video device for the system. It will detect and use a VGA device if there is one, otherwise it will try to use a TGA (21030) video device. Failing that, it will assume that there is no graphics device. The BIOS emulation that the standard, pre-built, images include is Digital's own BIOS emulation which supports most, if not all, of the standard graphics devices available.
