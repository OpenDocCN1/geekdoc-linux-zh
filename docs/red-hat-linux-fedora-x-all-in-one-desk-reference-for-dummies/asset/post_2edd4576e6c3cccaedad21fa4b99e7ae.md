
# Starting the Fedora Core Installation

- 10. When you're satisfied with the size of the new partition, press Enter.

FIPS displays the modified partition table and prompts you to press the C key to continue or the R key to reedit the partition table.

- 11. Press C to continue.

FIPS displays some information about the disk and whether you want to write the new partition information to the disk.

- 12. Press the Y key.

- 13. Remove the disk from the A drive and reboot the PC.

When the system comes back up, everything on your hard drive is intact, but the C drive is smaller. That's because you created a new partition from the unused parts of the old drive.

- 14. Choose Start:Programs:Accessories:System Tools:ScanDisk to run ScanDisk.

Running this program ensures that Windows gets adjusted to the size of the C drive.

You don't do anything with the newly created partition under DOS. Later, before Fedora Core installation, you create two or more Linux partitions of this partition.

After you use FIPS, Windows may assign drive letters to other disk and DVD-ROM drives on your PC. (For example, your D drive may be E.) FIPS makes sure, however, that the C drive remains C, so you can boot your system after FIPS splits the partitions. Remember these different drive names (for example, instead of D) when you want to get programs and files on drives other than C. Keeping a list of them couldn't hurt, at least until you get used to them.

# Starting the Fedora Core Installation

To install Linux, insert the DVD in the DVD drive and restart your PC (in Windows choose:Shutdown and then select Restart from the dialog box). If you are using CDs, the installation steps are the same as for the DVD except that you have to swap CDs when prompted by the installation program.

Most new PCs can boot directly from the DVD drive, but some PCs may require intervention from you. Typically, the PC may be set to boot from the hard drive before the DVD/CD drive and you have to get into SETUP to change the order of boot devices. To set up a PC to boot from the DVD

# 40 Selecting Keyboard, Mouse, and Installation Type

drive, you have to go into SETUP the PC powers up. The except steps for entering SETUP and setting the boot device vary from one PC to the next, but typically they involve pressing a key such as F2. As the PC powers up, a brief message tells you which key to press to enter SETUP. When you're in SETUP, you can designate the DVD drive as the boot device. After your PC is set up to boot from the DVD drive, simply put the DVD in the DVD drive and restart your PC.

![](img/d9230b719dc0efd80851f363d8c6f571_66_0.png)

After your PC powers up, the text screen displays a welcome message and a boot: The welcome message tells you that help is available by pressing one of the keys F1 through F5. To start installing Fedora immediately, press Enter. You can also enter other options at the boot prompt. For example, type linux mediacheck to test the DVD media for any presence. After the media check, you can continue with the installation. If you want to install Fedora Core with the new Security Enhanced Linux (SELinux) extensions enabled, type selinux at the boot: prompt.

Installing Fedora Core from the companion DVD-ROM or a fast (400MHz or better) Pentium PC takes about an hour or so, if you install nearly all packages.

The Fedora Core installation program probes — attempts to determine the presence — specific hardware and tailors the installation steps accordingly. For, if the installation program detects a network card, the program automatically displays the screens to configure your PC to work with the network in Linux. You may see a different sequence of screens from what I show in this chapter: the exact sequence depends on your PC's specific hardware configuration.

![](img/d9230b719dc0efd80851f363d8c6f571_66_1.png)

If you run into any problems during the installation, turn to Chapter 3 of this minibook. That chapter shows how to troubleshoot common installation problems.

# Selecting Keyboard, Mouse, and Installation Type

This first phase of the installation is where you go through a number of steps before moving to create the disk partitions for Fedora Core. Here are the steps in the first phase:

# Selecting Keyboard, Mouse, and Installation Type

1. The installation program displays a list of languages that you can use for the rest of the installation. Use your mouse to select the language you want from the list and then click Next to the next step.

Each screen has help available on the left side of the screen. You can read the help message to find out more about what you're supposed to do in a specific screen.

2. The installation program displays a list of keyboard layouts, as shown in 2-1.

Select a keyboard layout suitable for your language's character set (for example, U.S. English in the United States) and then click Next to continue.

3. The installation program displays a screen from which you can configure the mouse in your system.

A treelike list shows the mouse types, organized alphabetically by manufacturer. You need to know your mouse type or the PS/2 port (the small, round connector). If the name of your mouse appears in the list, select it. Otherwise a generic mouse type. Most new PCs have a PS/2 mouse. For a two-button mouse, select the Elite Button. Because X applications assume you're using a three-button mouse, select the Elite Button if you have a two-button mouse.

The Fedora Core installer tries to detect the mouse. If it fails, you may have to select a generic mouse type.

4. The installation program displays a screen from which you can configure the mouse. If it fails, you may have to select a generic mouse type.

5. The installation program displays a screen asking whether you want to install a new system or upgrade an older Fedora Core installation. For maximum flexibility, select the Custom installation. That way you can select only the packages you want to try out.

