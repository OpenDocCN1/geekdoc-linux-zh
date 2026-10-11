
## PCI Bus

The PCI bus is by far the most popular one for SCSI host adapters today, or at least for host adapters that are used for hard disks and other high-performance SCSI devices. You can purchase PCI SCSI boards that implement everything from Fast SCSI-2 through Ultra3 Wide SCSI in PCI form, although choices on the low end of the performance scale are slim.

The vast majority of PCI SCSI cards are DMA bus mastering devices, so you can generally count on these cards to produce little in the way of CPU load. How much you should spend on a PCI SCSI card depends largely on your needs. A low-end card, such as the Adaptec 2910, might be adequate for devices such as SCSI zip drives and scanners. Boards of this class support Fast SCSI-2 and typically cost less than $100. If you intend to ever attach a hard disk to your SCSI bus, however, I recommend buying something that supports at least Ultra2 Wide SCSI for 80MB/s transfers. A device of this type also offers the advantage of longer cable lengths, assuming you use LVD devices exclusively. Host adapters capable of supporting Ultra2 Wide SCSI typically cost more than $100, and sometimes as much as $400. One drawback to the high-end adapters is that they frequently don’t support the older 50-pin SCSI interfaces. Adding adapters to your SCSI chain can degrade performance and, perhaps just as important, reduce SCSI cable length limits. One solution to this dilemma is to use two SCSI host adapters. That might be unpalatable unless you need to use so many SCSI devices that one host adapter is inadequate to the task. Another alternative is to use a dual-interface SCSI host adapter, such as the ASUS SC-896. Such a product enables you to run two independent SCSI chains from a single SCSI host adapter.

Most PCI SCSI host adapters on the market are designed for use on x86 computers, but some can be used on other architectures as well, or come in variants for other architectures. If you want to use such a board on a Macintosh, Alpha PC, or some other system, be sure to check with the board manufacturer about compatibility. It’s also important that you check whether the Linux drivers for the product work in your target architecture; some drivers include assumptions specific to the x86 architecture.

### Oddball Connectors

Aside from the usual form of a SCSI host adapter on an expansion card, there are other forms the interface can take. These include

- **Motherboard SCSI support** Some high-end motherboards include SCSI support. Such support actually does fall into one of the categories I’ve described earlier; instead of using a physical expansion card socket, the SCSI host adapter circuitry resides on a virtual expansion card socket. Think of it as an expansion card that you can’t unplug. Today, such SCSI support invariably uses the PCI bus, although some earlier motherboards might use the EISA or VL-Bus instead.

- **Parallel-port SCSI** A few parallel-to-SCSI converters are available. These enable you to use external SCSI devices on computers that don't have their own SCSI host adapters. Unfortunately, the speed of these interfaces is quite limited, so they're not useful for anything but the slowest SCSI devices. Linux support is also limited; one of the few such devices supported by Linux is the one built into parallel-port Iomega zip drives.

- **USB SCSI** As with parallel-port SCSI host adapters, some adapters are available in USB form. Speed is likely to be poor when using these devices, and Linux support is uncertain at best. I recommend you check http://www.linux-usb.org/ for information on such devices before buying one.

- **PC-Card SCSI** Yet another adapter enables you to connect SCSI devices through a notebook computer's PC Card slot. This is a better option than a parallel-to-SCSI or USB-to-SCSI adapter for most notebook computers. Linux includes support for most PC-Card SCSI adapters. Check the PCMCIA HOWTO (included with all major Linux distributions) for details.

## SCSI Adapter Boards and Chipsets

When you know what sort of SCSI host adapter you want to buy, it's time to decide on a *specific* product. As with many hardware buying decisions for Linux, this task often boils down to one of deciding what *chipset* you need, and then locating a product that uses the chipset. Some of the largest names in the SCSI world, however, manufacture both chipsets and SCSI host adapters, so in some cases this task is easier than it is with some other products. No matter what chipset you select, you should also check on the BIOS support included on the SCSI host adapter. This support determines whether you can boot from a SCSI hard disk, and also determines some of the extra features available in the host adapter, such as cylinder/head/sector (CHS) geometry options and low-level disk formatting options.

## Popular Products in Linux

SCSI host adapters and chipsets from a handful of manufacturers are most popular in Linux, and seem likely to remain so in the near future. These products are all well supported in Linux, and some of these manufacturers help with Linux driver development, either by providing information to Linux developers or by developing drivers in-house. These products include

- **Adaptec boards** Most Adaptec (http://www.adaptec.com) host adapters work well in Linux. The Adaptec product line ranges from low-end ISA host adapters to top-of-the-line Ultra3 Wide SCSI products. Some motherboards that host integrated SCSI host adapters use Adaptec chipsets. Adaptec used to stink with Linux driver development support, but switched to a more supportive policy in 1998.

- **Advansys boards** Advansys (http://www.advansys.com) has written its own Linux drivers, which have been incorporated into the Linux kernel. The Advansys product line isn't quite as broad as is Adaptec's; current Advansys products are all PCI-based, and only go as far as Ultra2 Wide SCSI, although future products might exceed this limit.

- **Initio chipsets** Initio (http://www.initio.com) has developed a series of PCI SCSI chipsets that it uses on its own boards, and that are used on products from other manufacturers, such as SIIG (http://www.siig.com) and ASUS (http://www.asus.com). Initio's chipsets don't currently support the fastest SCSI standards, but they do support up to Ultra2 Wide SCSI. Initio wrote its own Linux drivers, which are now part of the standard Linux kernel.

- **MyLex boards** Formerly known as BusLogic, MyLex (http://www.mylex.com) products have long been favored in Linux because of the stability and completeness of the Linux drivers. (Third parties wrote the drivers with support from MyLex.) To reach Ultra3 performance levels with MyLex products, it's necessary to purchase a host adapter with built-in redundant array of independent disks (for more information on RAID, see Chapter 5) technology.

- **Symbios chipsets** Symbios (http://www.symbios.com), which used to be a division of NCR, sells a set of SCSI chipsets that are very popular in low-cost SCSI host adapters available from a wide variety of manufacturers, such as ASUS (http://www.asus.com) and J-Bond (http://www.jbond.com). Symbios also sells host adapters based on its own chipsets, and its chipsets find their way into some SCSI-equipped motherboards. The Symbios PCI chipsets have long been supported in Linux by two independent SCSI drivers, although only one (the sym53c8xx driver) is being maintained. Some Symbios chipsets are designed for ISA boards, but these chips are rare; it's the Symbios PCI products that are of most interest to the Linux community. These products range all the way through Ultra3 Wide devices.

You should check for Linux compatibility before purchasing a product from any of the preceding companies. A few more obscure chipsets from these companies might not be supported, and it's also possible that the latest product might not work with an older driver.

## Checking for Linux Compatibility

One way to check for Linux compatibility with a specific chipset is to do a kernel configuration and examine the boards and chipsets listed as options for SCSI host adapters, as shown in Figure 9.7. In some cases, the name of the driver corresponds exactly to the name of the product you are considering, in which case the decision is easy. In other cases, however, you must determine what chipset you use, or you must check the driver source code file (in `/usr/src/linux/drivers/scsi`). Somewhere in the source code file you can generally find a list of the specific boards or chipsets handled by the driver.
