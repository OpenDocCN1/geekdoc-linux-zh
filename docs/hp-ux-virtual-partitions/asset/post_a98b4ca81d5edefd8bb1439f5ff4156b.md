
## Separate vPars File Systems

This application will be loaded in every vPar in which it is to be run and consume the disk space associated with it. This is true for all applications.

Issuing `swlist` on this vPar shows all applications that have been loaded on it, including vPars software and the Broadvision application:

```
# swlist
# Initializing...
# Contacting target "actapppd1"...
# Target: actapppd:/
#
#
# Bundle(s):

B9788AA					1.3.0.01					Java 2 SDK 1.3 for HP-UX (700/800),
FA1-*					PA-1 + DX2.0 Add On

BUNDLIB11					B.11.11.0102.2			Required Patch Bundle for HP-UX 11i
CDS-English				B.11.11
FDDI-00					B.11.11.01				PCI FDDI;Support MWA3739A/A3739B;SW=3626A
FibChani-00					B.11.11.01.16			Support HSC/FibreChannel;
GOLDAPPS11				"B.11.11.0106.9 Gold Application Patches
GLDDABASE11				B.11.11.0106.9 Gold Base Patches for HP-UX 11i, June 2001
GIgChec-00				B.11.11.14				PCI/HSC Gigabit;Support
HW-AS55A					HW-AS42xA/AS439A/AS424A/AS45xA/SW=31642A
HPUXLII-OS-MC				B.11.11.0106				HP-UX Mission Critical
HPUXBase64				B.11.11				HP-UX 64-bit Base OS
HPUXBaseAux				B.11.11.0106				OP-UX Base OS Auxiliary
HW-enable11				B.11.11.0106				Hardware Enablement Patches for
									HP-UX 11i, June 2001
ITX-Recovery				B.3.3.116				Ignite-UX network recovery tool subset
QS235BA					B.04.13				Metascape Directory Server v4 for HP-UX
Onlinedlag				B.11.11.04				HPUX 11.11 Support Tools Bundle, Jun 2001
RAID-00					B.11.11.01				PCI RAID; Support HW-AS55A
#
# Product(s) not contained in a Bundle:
#

BVISION1				6.0				BroadVision One-To-One Enterprise
BVSNC-0AA				6.0.0				BroadVision One-To-One Enterprise 6.0_Patch AA
BVSNCeServerC2BMK7				6.0.0				BroadVision 1.1 Business-To-Business Contract Utility Installation
BVSNTreadingConnector				6.0.0				BroadVision 1.1 Adapter TradingConnector Application Installation
BVSNZbZ				6.0.0				BroadVision 1.1 Commerce Business-To-Business Installation
BVSNZb2AA				6.0.0-AA				BroadVision 1.1 Commerce Business Commerce Patch AA Installation
BVSNcwaa				6.0.0				BroadVision 1.1 Core Commerce Installation
BVSNcwaaa				6.0.0-AA				BroadVision 1.1 Core Commerce Base Commerce Patch AA Installation
BVSNcabv				6.0.0-AB				BroadVision 1.1 Core Commerce Patch AB Installation
BVSNVERITY261				2.6.1.0				Verity V2.6.1 Developer Kit
PHKL_23578				1.0				Software Distributor Cumulative Patch
PHKL_24625				1.0				Virtual Partitions manages cumul patch
PHKL_24546				1.0				vPar enablement patch
PHKL_24547				1.0				vPar enablement patch
PHKL_24548				1.0				vPar enablement patch
PHKL_24549				1.0				vPar enablement patch
PHKL_24550				1.0				Early boot, panic, Paeta & vPar enablement
PHKL_24551				1.0				thread cscop, vPar, Paeta, load averages
PHKL_24552				1.0				vPar enablement patch
PHKL_24553 1.0 console, chassis code, crash/dump, vPar PHKL_24554 1.0 vPar enablement patch PHKL_24555 1.0 PREFSETH LOCK 1/0, PR 8702 2.2, vPar PHKL_24556 1.0 vPar enablement patch PHKL_24557 1.0 vVar enablement patch PHKL_24559 1.0 vVar enablement patch PHKL_24559 1.0 SysLog overflow, high temp alerts, vPar PHKL_24560 1.0 vPar enablement patch PHKL_24561 1.0 Psetc & vVar Enablement PHKL_24562 1.0 vvar enablement patch PHKL_24563 1.0 vPar enablement patch PHKL_24564 1.0 vPar enablement patch PHKL_24565 1.0 vvar enablement patch PHKL_24566 1.0 Kernel Memory allocation, Faets Enablement PHKL_24570 1.0 Boot Bank, Faets & vPar enablement PHKL_24582 1.0 iSCSI Supports, Faets Enablement Patch PHKL_24585 1.0 Paets & vPar enablement patch PHKL_24985 1.0 vPar enablement patch PHKL_25080 1.0 vPar enablement patch FMBS_22535 1.0 Cumulative STRAAMS Patch FMNS_22713 1.0 iDGI) and linker tools cumulative patch Tivem 4.1.2 Tivol) Storage Manager make 3.60 00 06 HP-UX Virtual Partitions Functionality b 3.79.1 make
```

The revision of VirtualPartition software you see on your system will be later than that shown in the example.

Maintaining additional HP-UX file systems, which is probably going to be the case when you run vVars, requires you to think about the additional disk space required as well as techniques to ensure that your systems run smoothly such as recovery and operating system and application updates. Be sure to have a current inventory of your systems and perform backups and create bootable recovery tapes often.

## Non-vPar-Specific Section of Chapter: Introduction

In this section of the chapter we’ll focus on the following:

- Veritas Volume Manager overview
- Logical Volume Manager (LVM) - You will probably be using LVM to manage the data on your system. I provide LVM background in this section.
- Example of adding XP 256 disks to your system using LVM.
- Example of Using LVM to Reconfigure Disks - I include an example of a complex disk reconfiguration performed on a real system to show how many LVM commands are used. Although this disk reconfiguration may not be required on your system(s), it is a good example of using LVM commands.
- Some additional file-system commands.

## Veritas Volume Manager

New to HP-UX 11i is the Veritas Volume Manager, which is bundled with the operating system.

Unlike Logical Volume Manager, most of the work you perform with Veritas Volume Manager is performed through the Java-based graphical interface. The examples in this section all use the graphical interface to introduce you to Veritas Volume Manager.

## Logical Volume Manager Background

Logical Volume Manager is a disk management subsystem that allows you to manage physical disks as logical volumes. This means that a file system can span multiple physical disks. You can view Logical Volume Manager as a flexible way of defining boundaries of disk space that are independent of one another. Not only can you specify the size of a logical volume, but you can also change its size if the need arises. This possibility is a great advancement over dedicating a disk to a file system or having fixed-size partitions on a disk. Logical volumes can hold file systems, raw data, or swap space. You can now specify a logical volume to be any size you wish, have logical volumes that span multiple physical disks, and then change the size of the logical volume if you need to do so!

So what do you need to know in order to set up Logical Volume Manager and realize all these benefits? First, you need to know the terminology, and second, you need to know Logical Volume Manager commands. As with many other system administration tasks, you can use SAM to set up Logical Volume Manager for you. In fact, I recommend that you use SAM to set up Logical Volume Manager on your system(s). But, as usual, I recommend that you read this overview and at least understand the basics of Logical Volume Manager before you use SAM to set up Logical Volume Manager on your system. The SAM chapter (Chapter 11) has an example of using SAM to create logical volumes. After reading this section, you may want to take a quick look at that example.

For use with the Journaled Filesystem (JFS), Hewlett-Packard has an add-on product called HP OnLineJFS. This handy product allows you to perform many of the LVM functions without going into single-user mode. For example, when a filesystem needs to be expanded, the logical volume on which it resides needs to be unmounted before the expansion takes place. Normally, that unmounting would mean shutting the system down into single-user mode so that no user or process could access the volume and it could then be unmounted. With OnLineJFS, the logical volumes and file systems are simply expanded with the system up and running and no interruption to users or processes.

## Logical Volume Manager Terms

The following terms are used when working with Logical Volume Manager. They are only some of the terms associated with Logical Volume Manager, but they are enough for you to get started with Logical Volume Manager. You can work with Logical Volume Manager without knowing all these terms if you use SAM. It is a good idea, however, to read the following brief overview of these terms if you plan to use Logical Volume Manager, so you have some idea of what SAM is doing for you.
