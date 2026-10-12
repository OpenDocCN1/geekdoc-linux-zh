
## FIGURE 2.2
The Welcome screen.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_80_0.png)

The first screen you see is the Language Selection screen. It asks you which language you would like to use during the installation process. The default is English, but other options include Czech, Danish, Finnish, French, German, Italian, Norwegian, Romanian, Serbian, Slovak, Swedish, and Turkish. Select the Next button to continue. If you booted from a floppy, use the arrow keys to highlight your choice and press the Tab key to move to the OK button. Press Enter to continue using that selection.

The next screen is Keyboard Configuration. This step is a bit different depending on how you booted. The floppy disk boot asks you simply which keyboard layout you are using. Select which one you have and press OK to continue. If you booted directly from the CD, you will have three list boxes for Model, Layout, and Enable Dead Keys. Select the options that match your system and test it in the text box at the bottom of the screen. After your configuration is complete, press the Next button.

Most likely you will have chosen to boot from CD-ROM. If you have, you will see the Mouse Configuration screen next. If you booted from floppy you will be presented with a screen to select installation from the hard drive or CD-ROM. Select CD-ROM and press OK. You will be prompted to insert the CD-ROM into your drive if it is not already there. If you booted using another method such as a network install or floppy the system will scan for your mouse and load you into the graphical mode GUI at this point.

Unless you selected a full text install (or do not have a mouse) the Mouse Configuration screen is displayed. Select the type of mouse that you are using. You also have the option to check the Emulate 3 Buttons option if you have a two-button mouse. When you have made your selection, press Next.

You have now completed the Installation Program setup and are presented with the Welcome to Red Hat Linux system installer screen.

## The System Installer

This part of the install is where you get to select what type of install (workstation, server, custom) you would like to do, the programs you would like to install, and system configuration.

## New or Upgrade?

The installation program now asks whether you are installing a new system or upgrading a system that already contains Red Hat Linux 2.0 or greater. You are installing a new system, so highlight Install and press Enter.

There are three classes of installation: Workstation, Server, and Custom. By default the Workstation class is selected. As you go along, I’ll point out the differences between the Workstation and Server classes. Select which installation you would like to do and press Next.

## Partitioning

Because this is a new installation, the system installer assumes you do not have your Linux partitions set up. It does, however, give the following warning:

> You are about to erase any preexisting Linux installations on your system. If you don’t want to do this, you can continue with this install by partitioning manually, or you can go back and perform a fully customized installation.

This warning should be heeded, because it will indeed write over any previously installed Linux partitions. You should only get this warning if the system sees Linux partitions already present on your system.

> **Caution**
> If you install as a Server class, all of your partitions will be overwritten. This means you lose whatever else is on the disks—including other operating systems.

If you do have a Linux partition and you did not choose Custom, the system assumes you want to use the same partitions for the new system and begins to overwrite what is already there.

> **Note**
> This means you can install more than one version of Linux on your system, but you must custom install any after the first.

If you are performing a new install (and you did not previously have a Linux partition), or if you chose Custom, you are next prompted to partition your disks. Depending on which install you selected you will be given the option to Automatically partition your drives (except in custom install) or Manually partition using Disk Druid or fdisk. It is recommended that if you are going to manually partition your drives that you use Disk Druid. You should only use fdisk if you are familiar with using it.

Make your partition selection. If you selected automatic partitioning, it will skip the next few screens and bring you to the Network Configuration screen (provided you have a network device installed). If you choose to manually partition your drives follow the information in the previous section on partitioning using the interface you select. After you partition your drives, you will be prompted to choose the partitions you wish to format. You also have the option to check for bad blocks while formatting. It is recommended that you do this, but it will increase the time it takes to format your drives. Next you are asked to configure the Linux Loader.

## Configuring LILO

The next screen presents you with possible startup loader locations. A comment ensures that you do not overwrite the correct one. The choices are the Master Boot Record and the First Sector of Boot Partitions.

The Master Boot Record is the entire system's boot record. Replacing this causes LILO to start every time the system starts.

The First Sector of Boot Partitions can be used if you have another bootloader on your system. If these loaders are already in the primary drive's Master Boot Record, you probably do not want to replace them. (For more information refer to Chapter 3.)

If your system has SCSI drives, or you want to install LILO on a partition with more than 1023 cylinders, it may be necessary to enable the option to Use Linear Mode. If it is not, enabling this option shouldn't hurt anything, so it is probably a good idea to do so.

A few systems need to pass special options to the kernel at startup time in order for the system to function properly. If you need to pass startup options to the kernel, enter them at the next screen. The second part of bootloader states that it can start other operating systems that are on your system. If you have Windows 95 or 98, bootloader recognizes this and gives it a DOS startup label.

Press Next when you have made your selections. More often than not, you will just be able to accept the default selections.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_82_0.png)

# PART I

## Network Configuration

If you have one or more network interface cards (NIC) installed this next screen will allow you to enter configurations for each one. If you do not have a network card installed you may not see this screen at all.

Enter the IP address, netmask, network, and broadcast IPs for each NIC (or select the DHCP option if you have a DHCP server on your network). Also enter in the hostname for your system as well as its gateway and DNS addresses.

There is also an option for you to Activate on Boot. This will activate that NIC upon boot. You will have to manually start that interface once the system is booted if this is not selected. The install does probe your network cards but is not guaranteed to always be correct. If your card does not seem to be functioning after your install, you can go back in and change which driver your card is using, as well as all of these options.

Once you have filled this in, press Next to continue configuring your system.

If you do not want to configure your NIC at this moment, you can easily do it later after the install.

## Setting the Time Zone

You are next asked to set up your system’s time zone. You can simply mouse over the map, find your location, and click to select your time zone. Also, you may just select the correct time zone from the list box under the map. If you want to configure this by selecting your Universal Time Coordinated (UTC) offset, you can select that tab and find your offset in that list box. Press Next when you are ready to move to the Account Configuration portion of the setup.

## Setting the root Password and the root Account

The root account has no limitations; therefore, the password for this account must be kept secure. You are asked to enter a password twice. The password must be at least six characters long. As you type in this new password, notice that the typing is hidden with "**". This is a security feature. You enter the password into the system twice to make sure you typed it correctly. The root password should be alphanumeric and a mixture of upper- and lowercase characters to make it harder for hackers to guess.

root is the all-powerful administrative account and is the most privileged account on a Linux system. This account gives you the ability to carry out all facets of system administration, including adding accounts, changing user passwords, examining log files, installing software, and so on. When using this account it is crucial to be as careful as possible. The root account has no security restrictions imposed upon it. This means it is
