
described shortly, reducing the odds of an unused device interfering with the hardware you do use.

## **FIGURE 3.1** The BIOS setup screen provides features related to low-level hardware configuration.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_167_0.png)

Precisely how to disable hardware in the BIOS varies from one computer to another. You should peruse the available menus to find mention of the hardware you want to disable. Menus entitled *Integrated Peripherals* or *Advanced* are particularly likely to hold these features. Once you've spotted the options, follow the on-screen prompts for hints at how to proceed; for instance, Figure 3.1 shows an *Item Specific Help* area on the right side of the screen. Information about keys to press to perform various actions appears here. Once you're finished, follow the on-screen menus and prompts to save your changes and exit. When you do so, the computer will reboot.

Once Linux boots, it uses its own drivers to access the computer's hardware. Understanding the hardware resources that Linux uses will help you determine when you may want to shut down, boot into the BIOS, and disable particular hardware devices at such a low level.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_167_1.png)

### Real World Scenario

#### Booting Without a Keyboard

Most PCs have keyboards attached to them; however, many Linux computers function as servers, which don't require keyboards for day-to-day operation. In such cases, you may want to detach the keyboard to reduce clutter and eliminate the risk of accidental key-presses causing problems.

Unfortunately, many computers complain and refuse to boot if you unplug the keyboard and attempt to boot the computer. To disable this warning, look for a BIOS option called *Halt On* or something similar. This option tells the BIOS under what circumstances it should refuse to boot. You should find an option to disable the keyboard check. Once you select this option, you should be able to shut down, detach the keyboard, and boot normally. Of course, you'll need to be able to access the computer via a network connection or in some other way to administer it, so be sure this is configured before you remove the keyboard!

### IRQs

An *interrupt request* (IRQ), or interrupt, is a signal sent to the CPU instructing it to suspend its current activity and to handle some external event such as keyboard input. On the x86 platform, IRQs are numbered from 0 to 15. More modern computers, including x86–64 systems, provide more than these 16 interrupts. Some interrupts are reserved for specific purposes, such as the keyboard and the real–time clock; others have common uses (and are sometimes overused) but may be reassigned; and some are left available for extra devices that may be added to the system. Table 3.1 lists the IRQs and their common purposes in the x86 system. (On x86–64 systems, IRQs are typically assigned as in Table 3.1, but additional hardware may be assigned to higher IRQs.)

**TABLE 3.1 IRQs and Their Common Uses**

| IRQ | Typical Use | Notes |
|---|---|---|
| 0 | System timer | Reserved for internal use. |
| 1 | Keyboard | Reserved for keyboard use only. |
| 2 | Cascade for IRQs 8–15 | The original x86 IRQ–handling circuit can manage just 8 IRQs; 2 are tied together to handle 16 IRQs, but IRQ 2 must be used to handle IRQs 8–15. |
| 3 | Second RS–232 serial port (COM2: in Windows) | May also be shared by a fourth RS–232 serial port. |
| 4 | First RS–232 serial port (COM1: in Windows) | May also be shared by a third RS–232 serial port. |
| 5 | Sound card or second parallel port (LPT2: in Windows) | |
| 6 | Floppy disk controller | Reserved for the first floppy disk controller. |
| 7 | First parallel port (LPT1: in Windows) | |
| 8 | Real-time clock | Reserved for system clock use only. |
| 9 | Open interrupt | |
| 10 | Open interrupt | |
| 11 | Open interrupt | |
| 12 | PS/2 mouse | |
| 13 | Math coprocessor | Reserved for internal use. |
| 14 | Primary ATA controller | The controller for ATA devices such as hard drives; typically /dev/hda and /dev/hdb under Linux. |
| 15 | Secondary ATA controller | The controller for more ATA devices; typically /dev/hdc and /dev/hdd under Linux. |

The original *Industry Standard Architecture* (ISA) bus design makes sharing an interrupt between two devices tricky. Ideally, every ISA device should have its own IRQ. The more recent *Peripheral Component Interconnect* (PCI) bus makes sharing interrupts a bit easier, so PCI devices frequently end up sharing an IRQ. The ISA bus has become rare on computers made since 2001 or so, but it’s common on older computers. Even some computers that lack physical ISA slots may use ISA internally to manage some devices, such as RS-232 serial ports and parallel ports.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_169_0.png)

Once a Linux system is running, you can explore what IRQs are being used for various purposes by examining the contents of the `/proc/interrupts` file. A common way to do this is with the use of the `cat` command:

```
$ cat /proc/interrupts
           CPU0
0:         42  IO-APIC-edge      timer
1: 444882 IO-APIC-edge i8042
4: 12 IO-APIC-edge i8042
6: 69 IO-APIC-edge floppy
8: 0 IO-APIC-edge rtc
9: 0 IO-APIC-fasteoi acpi
14: 3010291 IO-APIC-edge ide0
15: 11156960 IO-APIC-edge ide1
16: 125264892 IO-APIC-fasteoi eth0
17: 0 IO-APIC-fasteoi cx88[0], cx88[0]
20: 3598946 IO-APIC-fasteoi sata_via
21: 4566307 IO-APIC-fasteoi uhci_hcd:usb1, uhci_hcd:usb2, ehci_hcd:usb3
22: 430444 IO-APIC-fasteoi VIA8237
NMI: 0 Non-maskable interrupts
LOC: 168759611 Local timer interrupts
TRM: 0 Thermal event interrupts
THR: 0 Threshold APIC interrupts
SPU: 0 Spurious interrupts
ERR: 0
```

> **NOTE** The `/proc` file system is a virtual file system — it doesn't refer to actual files on a hard disk, but to kernel data that's convenient to represent using a file system. The files in `/proc` provide information about the hardware, running processes, and so on. Many Linux utilities use `/proc` behind the scenes; or you can directly access these files using utilities like `cat`, which copies the data to the screen when given just one argument.

This output shows the names of the drivers that are using each IRQ. Some of these driver names are easy to interpret, such as `floppy`. Others are more puzzling, such as `cx88` (it's a driver for a video capture card). If the purpose of a driver isn't obvious, try doing a Web search on it; chances are you'll find a relevant hit fairly easily. Note that the preceding output shows interrupts numbered up to 22; this system supports more than the 16 base x86 interrupts.

> **WARNING** The `/proc/interrupts` file lists IRQs that are in use by Linux, but Linux doesn't begin using an IRQ until the relevant driver is loaded. This may not happen until you try to use the hardware. Thus, the `/proc/interrupts` list may not show all the interrupts that are configured on your system. For instance, the preceding example shows nothing for IRQ 7, which is reserved for the parallel port, because the port hadn't been used prior to viewing the file. If the parallel port were used and `/proc/interrupts` viewed again, an entry for IRQ 7 and the `parport0` driver would appear.

If your system suffers from IRQ conflicts, you must reconfigure one or more devices to use different IRQs. This topic is described shortly, in “Configuring Expansion Cards.”

### I/O Addresses

I/O addresses (also referred to as I/O ports) are unique locations in memory that are reserved for communications between the CPU and specific physical hardware devices. Like IRQs, I/O addresses are commonly associated with specific devices and should not ordinarily be shared. Table 3.2 lists some Linux device filenames along with the equivalent names in Windows, as well as the common IRQ and I/O address settings.

**TABLE 3.2 Common Linux Devices**

| Linux Device | Windows Name | Typical IRQ | I/O Address |
| :--- | :--- | :---: | :---: |
| /dev/ttyS0 | COM1 | 4 | 0x03f8 |
| /dev/ttyS1 | COM2 | 3 | 0x02f8 |
| /dev/ttyS2 | COM3 | 4 | 0x03e8 |
| /dev/ttyS3 | COM4 | 3 | 0x02e8 |
| /dev/lp0 | LPT1 | 7 | 0x0378-0x037f |
| /dev/lp1 | LPT2 | 5 | 0x0278-0x027f |
| /dev/fd0 | A: | 6 | 0x03f0-0x03f7 |
| /dev/fd1 | B: | 6 | 0x0370-0x0377 |

> **TIP**
> Although the use is deprecated, older systems sometimes use `/dev/cuax` (where x is a number from 0 and up) to indicate an RS-232 serial device. Thus, `/dev/ttyS0` and `/dev/cua0` refer to the same physical device.

Once a Linux system is running, you can explore what I/O addresses are being used by examining the contents of the `/proc/ioports` file. A common way to do this is with the `cat` command:

```
$ cat /proc/ioports
0000-001f : dma1
0020-0021 : pic1
```
