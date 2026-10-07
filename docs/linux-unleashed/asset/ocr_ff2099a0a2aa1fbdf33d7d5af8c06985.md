Alternatively, you should check the settings of every device in your system for conflicts. Usually, network cards conflict with sound boards, non-SCSI tape driver cards, video cards, and similar add-on cards. Most cards use DIPs or jumpers to set these parameters, so check them against the documentation. To help isolate the problem, remove cards that are not necessary, such as a sound card, and see whether the boot process moves past the device that caused the hangup.

Another problem that can occur is with SCSI devices (and a few others, although much rarer), which must have specific settings in the kernel image. Some kernels were compiled with settings that are default values for adapters or disk drives, and if the settings have been changed, the kernel hangs. This is often the case with special-purpose kernels that have been developed for nonmainstream adapters. To check for this type of problem, investigate any documentation that came with the kernel image.

The most common devices in a PC (COM ports, parallel ports, and floppies) and their IRQ, DMA, and I/O addresses are shown in Table 3.1. These are the default values for a PC, but they may be changed by users. Because only two COM ports (serial ports) are usually supported by DOS, they share IRQ values. The I/O addresses are different, though. Both floppy disks share the same I/O addresses, IRQ, and DMA.

**TABLE 3.1. COMMON DEVICES IN A PC AND THEIR IRQ, DMA, AND I/O ADDRESSES.**

| **Device** | **IRQ** | **DMA** | **I/O address (hex)** |
| :--- | :---: | :---: | :---: |
| COM 1 (/dev/ttyS0) | 4 | N/A | 3F8 |
| COM 2 (/dev/ttyS1) | 3 | N/A | 2F8 |
| COM 3 (/dev/ttyS2) | 4 | N/A | 3E8 |
| COM 4 (/dev/ttyS3) | 3 | N/A | 2E8 |
| LPT 1 (/dev/lp0) | 7 | N/A | 378-37F |
| LPT 2 (/dev/lp1) | 5 | N/A | 278-27F |
| Floppy A (/dev/fd0) | 6 | 2 | 3F0-3F7 |
| Floppy B (/dev/fd1) | 6 | 2 | 3F0-3F7 |

Network cards, SCSI adapters, sound boards, video cards, and other peripherals all must have unique IRQ, DMA, and I/O addresses, which can be difficult to arrange with a fully loaded system. For more information on available values, check your device or card installation manual for recommended values and potential conflicts.