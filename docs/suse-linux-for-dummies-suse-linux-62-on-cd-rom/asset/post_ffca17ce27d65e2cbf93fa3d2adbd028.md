
## Chapter 3: Discovering What's in Your System

### Old systems and new disks

Disks are made up of cylinders of information, which in turn are made up of tracks of information, which in turn are made up of blocks of information. Newer disks have more than older computer systems can handle easily. Therefore, a method of logical addressing, or LBA, was created so that older computer systems could work with newer disks, which have more than 1,023 cylinders.

However, that changing your disk to LBA specification if it is not LBA already will make the data on the disk inaccessible. Therefore, before changing your disk to LBA, you should back it up if it contains any data. (You may decide that adding another disk is not such a bad idea as an expansion strategy.)

Different hardware systems have different ways to enter the BIOS setup. Usually, you can enter the BIOS when you turn on the power and start to boot; when you press the Reset button on the front of the system and start to reboot; when you go through the normal shutdown of your Windows system and ask to reboot.

The BIOS section for configuring hard disks typically indicates your computer system is capable of LBA. Your disk may already be accessed as an LBA disk. Some BIOS do this automatically the first time you use a disk with a large number of cylinders. Note,

![](img/96a9ce6a13d8d15ed05f867f41574278_66_0.png)

We strongly recommend that you put Linux on a separate disk. The task of shrinking MS-DOS and Windows small enough to allow Linux to reside in its full glory on an existing disk is difficult at best and impossible at worst.

If you follow our recommendation and buy another disk, put it the second disk on the first IDE controller or disk 1 on your SCSI controller, assuming that your existing Windows disk is either the first on your IDE controller or ID 0 on your SCSI controller. Adding disks is a hardware thing; the store where you buy the disk should be able to add it to your system for you. And while the system is there, you can ask the folks to tell you the details of the other hardware in your system.

While installing Linux on your disks, you might be asked to supply the number of disk heads (or tracks), the number of cylinders, and the number of sectors per track. Most modern disk drives provide this information on a paper label on the outside of the disk. Some modern disks are set up for Windows, and Linux can access the number of disk heads, cylinders, and sectors.

If you have your computer apart looking for other information (a pox on manufacturers who don't supply such useful information), you may as well down all the disk information you can find. You should look for the number of heads, cylinders, and sectors. This information is used to tell the operating system where to put data with respect to the beginning of the disk. If you have trouble, check out the "Getting Information from Windows 95" and "Getting Information from MS-DOS or Windows 3.1" sections. SCSI disk users Part II: Installing SuSE Linux don't have to supply this information because the SCSI controller and device drivers calculate it on the fly. SCSI disk owners should, however, know the size of their disks, which is printed on the disk or is available through the sections just mentioned.

### Getting Information from Windows 95

If you have Windows 95, you can use the msd program in MS-DOS mode as described in the next section to find out about the hardware in your system. Much more information is available, however, through the Control Panel in Windows 95.

With pencil and paper handy, it's time to get to the Control Panel and all that information. Follow along with these steps:

- 1. Click Start:Settings:Control Panel.
We use a shorthand method for showing menus. When you see a line such as the following:
Start:Settings:Control Panel
it means "Click the Start button, and then click the Settings menu item, and then click the Control Panel item."
- 2. Double-click the System icon and then click the Device Manager tab.
- 3. At the top of the screen, click to select the Devices by Connection option.
This shows all components and how they relate to each other. The screen looks similar to Figure 3-1.
If you have a printer attached to your system, at this point you can click Print in the System Properties dialog box. Then, under Type Report, click All Devices and System Summary. Click OK. This procedure prints a full report about your system. You will not have all the information you may need, such as which disk goes with which controller, but you will save a lot of writing.
- 4. In the list, click Computer.
- 5. Click the Properties button.
The View Resources tab of the Computer Properties dialog box appears.
- 6. Click to select the Interrupt Request (IRQ) option and write down the displayed information.
The left column, Setting lists interrupt requests, as shown in Figure 3-2. The hardware using a particular IRQ is listed in the right column. Note that no two different devices can use the same IRQ.

![](img/96a9ce6a13d8d15ed05f867f41574278_67_0.png)

![](img/96a9ce6a13d8d15ed05f867f41574278_67_1.png)

![](img/96a9ce6a13d8d15ed05f867f41574278_68_0.png)

Figure 3-1: Use the Device Manager tab to discover hardware details.

- 7. At the top of the screen, click to select the Direct Memory Access (DMA) option and copy the displayed information.
- 8. At the top of the screen, click to select the Input/Output (I/O) option and copy the pertinent information. Part II: Installing SuSE Linux

![](img/96a9ce6a13d8d15ed05f867f41574278_69_0.png)

Figure 3-2: Viewing interrupt request (IRQ) numbers.

- 9. Click Cancel.
The screen returns to the Device Manager tab of the System Properties box.

![](img/96a9ce6a13d8d15ed05f867f41574278_70_0.png)

Figure 3-3: When upper-level entries are preceded by a minus sign, as they are, you can see their subentries.

- 5. Click the Settings tab, write down the drive type, and then click Cancel.
The screen returns to the Device Manager tab of the System Properties box.
- 6. Write down the highlighted information, which is the type of disk.
- 7. For each disk subset that controller, repeat Steps 4 to 6.
- 8. Follow the same general steps for any other hard disk controller entries.
- 14. Finally, for the Sound, Video, and Game controllers entry, copy information on both the General tab and the Resources tab.
