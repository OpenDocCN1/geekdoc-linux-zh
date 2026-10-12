
existing DOS partition and create room for the Linux partition. Later on, during Red Hat Linux installation, you have to further divide the partition meant for Linux into at least two parts: one for the Linux root file system and the other for swap space.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_40_0.png)

Although you have no guarantee that FIPS will split a DOS partition successfully, you should consider using it to create room for Red Hat Linux — especially if you have a brand-new PC with only DOS and Windows installed on the hard disk. In this case, even if something goes wrong with FIPS, you can reinstall Windows and the applications.

The FIPS.EXE program and related files are located in the \DOSUTIL subdirectory of the companion CD-ROMs. To use FIPS, follow these steps:

- 1. For FIPS to work, all used areas of the disk must be contiguous — or at least as tightly packed as possible. You can prepare the disk for FIPS by running a defragmenter. How you defragment the hard disk depends on your current operating system. For example, in Windows 95/98, select Start ⇨ Programs ⇨ Accessories ⇨ System Tools ⇨ Disk Defragmenter.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_40_1.png)

You also should check the hard disk for errors by running a program such as Norton Disk Doctor in MS-DOS 6.0 or later (in Windows 95/98, use SCANDISK).

- 2. In MS-DOS 6.0 or later, create a bootable disk using the command FORMAT A: /S. In Windows 95/98, create a startup disk by using the Add/Remove Programs option in the Control Panel and then following the instructions in the Startup Disk tab.

- 3. Copy the following files from the CD-ROM to the formatted disk. (The following example assumes that D: is the CD-ROM drive.)

```
COPY D:\DOSUTIL\FIPS.EXE A:
COPY D:\DOSUTIL\RESTORRB.EXE A:
COPY D:\DOSUTIL\FIPSDOCS\ERRORS.TXT A:
```

FIPS.EXE is the program that splits partitions. ERRORS.TXT is a list of FIPS error messages. You consult this list for an explanation of any error messages displayed by FIPS. RESTORRB.EXE is a program that enables you to restore certain important parts of your hard disk from a backup of those areas created by FIPS.

- 4. Leave the bootable disk in the A: drive, and restart the PC. The PC boots from A: and displays the A> prompt.
- 5. Type **FIPS**. The FIPS program runs and shows you information about your hard disk. FIPS gives you an opportunity to save a backup copy of important disk areas before proceeding. After that, FIPS displays the first free cylinder where the new partition can start (as well as the size of the partition in megabytes).
- 6. Use the left and right arrow keys to adjust the starting cylinder of the new partition (the one that results from splitting the existing partition) to change the partition size. Press the right arrow to increase the starting cylinder number. This leaves more room in the existing partition and reduces the size of the new partition you create. Try to create a new partition that is 1GB or larger.
- 7. When you are satisfied with the size of the new partition, press Enter. FIPS displays the modified partition table and prompts you to enter **C** to continue or **R** to reedit the partition table.
- 8. Press **C** to continue. FIPS displays some information about the disk and asks whether you want to write the new partition information to the disk.
- 9. Press **Y**. FIPS writes the new partition table to the hard disk and then exits.
- 10. Remove the disk from the A: drive and reboot the PC.

When the system comes up, everything in your hard disk should be intact — but the C: drive will be smaller. You have created a new partition from the unused parts of the old C: drive.

You don’t do anything with the newly created partition under DOS. Later, during Red Hat Linux installation, you create two or more Linux partitions out of this new partition.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_41_0.png)

## Starting the Red Hat Linux Installation

To start the Red Hat Linux installation, put the Red Hat boot disk in your PC’s A: drive and restart your PC. (In MS-DOS 6.0 or later, press the reset button or press Ctrl+Alt+Delete; In Windows 95/98, select Start → Shutdown and then select Restart from the dialog box.) Your PC goes through its normal startup sequence, such as checking memory and running the ROM BIOS code. Then the PC loads Red Hat Linux from the boot disk and begins running the Red Hat installation program. The rest of the installation occurs under the control of the installation program.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_42_0.png)

As you power up or reboot the PC with the Red Hat boot disk, place this book’s companion CD-ROMs in the CD-ROM drive. That way the installation program can find and use the Red Hat Linux CD-ROMs to start the installation in graphical mode. Otherwise the installation program initially will start in text mode and prompt for the CD-ROM. Only then it will start the X Window System and switch to a graphical installation screen.

A few moments after you start the boot process, an initial screen appears. The screen displays a welcome message and ends with a boot: prompt. The welcome message tells you that more information is available by pressing one of the function keys F1 through F5.

If you want to read the help screens, press the function key corresponding to the help you want. If you don’t press any keys after a minute, the boot process proceeds with the loading of the Linux kernel into the PC’s memory. To start booting Red Hat Linux immediately, press Enter. After the Linux kernel loads, it automatically starts the Red Hat Linux installation program. This, in turn, starts the X Window System, which provides a graphical user interface for the installation.

If you have all the configuration information (such as video card, monitor, network card details, IP addresses, and host names for the TCP/IP network configuration) and all goes well, installing Red Hat Linux from the companion CD-ROMs on a fast (200MHz or better) Pentium PC should take 30 to 40 minutes. (This is assuming that you select nearly all packages.) For example, on a 200MHz Pentium PC with 64MB RAM and a 1GB-disk partition devoted to Red Hat Linux, the installation takes about 35 minutes. On older 486 PCs, the installation process may take somewhat longer.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_42_1.png)

During the installation, the Red Hat installation program probes — attempts to determine the presence of — specific hardware and tailors the installation steps accordingly. For example, if the installation program detects a network card, the program automatically displays the screens in which you can configure the TCP/IP network. This means you may see some variation in the sequence of steps depending on your specific hardware configuration.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_42_2.png)

If you run into any problems during the installation, refer to Session 4 to learn how to troubleshoot common installation problems.

As you get ready to install Red Hat Linux, You go through the following steps before moving on to disk setup in the next section and the actual installation of various packages in Session 3:

- 1. Assuming that you already placed this book’s companion CD-ROMs in the CD-ROM drive before starting the installation, the installation program starts the X Window System and displays a list of languages in a graphical installation screen. Use your mouse to select the language you want and then click the Next button to proceed to the next step.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_43_0.png)

In the graphical mode installation, each screen has online help available on the left side. You can read the help message to learn more about what you are supposed to select in a specific screen.

- 2. The installation program displays a list of keyboard types, as shown in Figure 2-1. Select a keyboard model that closely matches your PC’s keyboard. If you don’t see your keyboard model listed, select one of the generic models: Generic 101-key PC or Generic 104-key PC. (Newer keyboards with the Windows keys match this model.) Next, select a keyboard layout that depends on your language’s character set (for example, English in the United States). Finally, select the Enable dead keys option if the language you select has special characters that must be composed by pressing multiple keys in sequence. For the English language, you can safely select the Disable dead keys option.

- 3. The installation program displays a screen (see Figure 2-2) from which you can configure the mouse in your system. The various mouse types are listed in a tree structure organized alphabetically by manufacturer. You need to know your mouse type and whether it is connected to the PC’s serial port or the PS/2 port (a small round connector). If your mouse type appears in the list, select it. Otherwise, select a generic mouse type. Most new PCs have a PS/2 mouse. Finally, for a two-button mouse, you should select the Emulate 3 Buttons option. Because many X applications assume that you use a 3-button mouse, you should go ahead and select this option. On a typical 2-button mouse, you can simulate a middle-button click by pressing both buttons simultaneously. On a Microsoft Intellimouse, the wheel acts as the middle button.
