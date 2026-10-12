
10. When you're satisfied with the size of the new partition, press Enter.

FIPS displays the modified partition table and prompts you to press the C key to continue or the R key to reedit the partition table.

11. Press C to continue.

FIPS displays some information about the disk and asks whether you want to write the new partition information to the disk.

12. Press the Y key.

FIPS writes the new partition table to the hard disk and then exits.

13. Remove the disk from the A drive and reboot the PC.

When the system comes back up, everything on your hard drive is intact, but the C drive is smaller. That's because you created a new partition from the unused parts of the old C drive.

14. Choose Start::Programs::Accessories::System Tools::ScanDisk to run ScanDisk.

Running this program ensures that Windows gets adjusted to the new size of the C drive.

You needn't do anything with the newly created partition under DOS. Later, during Fedora Core installation, you create two or more Linux partitions out of this new partition.

> **WARNING!** After you use FIPS, Windows may assign different drive letters to other disk and DVD-ROM drives on your PC. (For example, your D drive may become E.) FIPS does make sure, however, that the C drive remains C, so you can boot your system after FIPS splits the partitions. Remember those different drive names (for example, E instead of D) when you want to get to programs and files on drives other than C. Keeping a list of them couldn't hurt, at least until you get used to them.

## Starting the Fedora Core Installation

To install Linux, insert the DVD in the DVD drive and restart your PC (in Windows choose Start::Shut down and then select Restart from the dialog box). If you are using CDs, the installation steps are the same as that for the DVD except that you have to swap CDs when prompted by the installation program.

> **REMEMBER** Most new PCs can boot directly from the DVD drive, but some PCs may require intervention from you. Typically, the PC may be set to boot from the hard drive before the DVD/CD drive and you have to get into SETUP to change the order of boot devices. To set up a PC to boot from the DVD drive, you have to go into SETUP as the PC powers up. The exact steps for entering SETUP and setting the boot device vary from one PC to the next, but typically they involve pressing a key such as F2. As the PC powers up, a brief message tells you what key to press to enter SETUP. When you're in SETUP, you can designate the DVD drive as the boot device. After your PC is set up to boot from the DVD drive, simply put the DVD in the DVD drive and restart your PC.

![](img/9f89727199836b0f871f1745838aa8b2_66_0.png)

After your PC powers up, it loads the Linux kernel from the DVD and the Linux kernel starts running the Fedora Core installation program. For the rest of the installation, you work with the installation program's GUI screens.

After a few moments, the text screen displays a welcome message and a *boot:* prompt. The welcome message tells you that help is available by pressing one of the function keys F1 through F5. To start installing Fedora Core immediately, press Enter. You can also enter other options at the *boot:* prompt. For example, type **linux mediacheck** to test the DVD media for any problems. Press Enter to perform the media check. After the media check, you can continue with the installation. If you want to install Fedora Core with the new Security Enhanced Linux (SELinux) extensions enabled, type **selinux** at the *boot:* prompt.

Installing Fedora Core from the companion DVD-ROM on a fast (400MHz or better) Pentium PC takes about an hour or so, if you install nearly all packages.

The Fedora Core installation program *probes* — attempts to determine the presence of — specific hardware and tailors the installation steps accordingly. For example, if the installation program detects a network card, the program automatically displays the screens needed to configure your PC to work with the network in Linux. You may see a different sequence of screens from what I show in this chapter; the exact sequence depends on your PC's specific hardware configuration.

![](img/9f89727199836b0f871f1745838aa8b2_66_1.png)

If you run into any problems during the installation, turn to Chapter 3 of this minibook. That chapter shows how to troubleshoot common installation problems.

## Selecting Keyboard, Mouse, and Installation Type

This first phase of the installation is where you go through a number of steps before moving on to create the disk partitions for Fedora Core. Here are the steps in the first phase:

**1. The installation program displays a list of languages that you can use for the rest of the installation.** Use your mouse to select the language you want from the list displayed and then click **Next** to proceed to the next step.

Each screen has online help available on the left side of the screen. You can read the help message to find out more about what you're supposed to do in a specific screen.

![](img/9f89727199836b0f871f1745838aa8b2_67_0.png)

**2. The installation program displays a list of keyboard layouts, as shown in Figure 2-1.**

Select a keyboard layout suitable for your language's character set (for example, U.S. English in the United States) and then click **Next** to continue.

**3. The installation program displays a screen from which you can configure the mouse in your system.**

A treelike list shows the mouse types, organized alphabetically by manufacturer. You need to know your mouse type and whether it's connected to the PC's serial port or the PS/2 port (the small, round connector). If the name of your mouse appears in the list, select it. Otherwise select a generic mouse type. Most new PCs have a PS/2 mouse. For a two-button mouse, select the **Emulate 3 Buttons** option. Because many X applications assume you're using a three-button mouse, select this option. (On a typical two-button mouse, you can simulate a middle-button click by pressing both buttons simultaneously. On a Microsoft Intellimouse, the wheel acts as the middle button.) Click **Next** after selecting the mouse.

The installer tries to detect the monitor and displays a screen with the results, whether or not it detects the monitor correctly (see Figure 2-2).

**4. If the Fedora Core installer displays a wrong monitor or a generic one as the choice, scroll through the list and pick the correct name of your monitor from the list.**

(One good thing about monitors is that you can always easily look up the make and model number on the back of the monitor.)

**5. The installation program displays a screen asking whether you want to install a new system or upgrade an older Fedora Core installation.** For a new Fedora Core installation, click **Install**. Then a screen (see Figure 2-3) prompts you for the installation type.

For a new installation, you have to select the installation type — Personal Desktop, Workstation, Server, or Custom. The Personal Desktop, Workstation, and Server installations simplify the installation process by partitioning the disk in a predefined manner. The Personal Desktop installation creates a Fedora Core system for home, laptop, or desktop use. A graphical environment is installed along with productivity applications.

![](img/9f89727199836b0f871f1745838aa8b2_68_0.png)

![](img/9f89727199836b0f871f1745838aa8b2_68_1.png)

![](img/9f89727199836b0f871f1745838aa8b2_69_0.png)

Figure 2-3: Select what type of installation you want.

A Workstation-class installation installs a graphical environment as well as software development tools. This type of installation also deletes all currently existing Linux-related partitions, creating a set of new partitions for Linux.

> **WARNING!**

A Server-class installation deletes all existing disk partitions, including any existing Windows partitions, and creates a whole slew of Linux partitions. Server-class installation does not install the graphical environment.

> **TIP**

For maximum flexibility, select the Custom installation. That way you can select only the packages you want to try out.

The next major phase of installation involves partitioning the hard disk for use in Fedora Core.

## Partitioning the Disk for Fedora Core

The Fedora Core installer displays a screen (see Figure 2-4) from which you can select a partitioning strategy.
