
## GIZMODO | UK

Not your average technology website

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_29_0.png)

## EXPLORE NEW WORLDS OF TECHNOLOGY
GADGETS, SCIENCE, DESIGN AND MORE

- Fascinating reports from the bleeding edge of tech
- Innovations, culture and geek culture explored
- Join the UK’s leading online tech community

www.gizmodo.co.uk

twitter.com/GizmodoUK facebook.com/GizmodoUK

## Escape Windows

The time has come – follow us as we help you evade Windows and make a bid for Linux and freedom.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_30_0.png)

> “Microsoft has finally lost the plot – now is the perfect time to switch to a better OS”

If, having bought a new PC that has Windows pre-installed, you've come to the conclusion that Microsoft has finally lost the plot, now is the perfect time to switch to a better OS. Macs are shiny and expensive, so why buy one when you can keep your existing PC and move to Linux? Gone are the days when Linux meant immersing yourself in command-line chicanery – we'll show you how you can install a user-friendly flavour of Linux alongside your existing Windows installation without losing any data, so you can dip your toes into the free and open waters of Linux. To make the transition as smooth as possible, we've chosen Ubuntu 14.04 LTS (on the cover disc) as our Linux distro of choice. Ubuntu is one of the most user-friendly Linux distros out there, and 14.04 LTS has just been released. LTS stands for Long Term Support, which means it gets five years of updates and support. Here's what you're going to do. Firstly, we would be remiss if we didn't instruct you about how to back up your current PC. You have two basic choices here: the backup tools which are built into Windows itself, or SystemRescueCD, which you'll find as part of the cover disc. Next, we'll explain how modern PCs ship with a new system called the UEFI, which may cause minor problems. But don't worry, because we'll show you how to overcome any issues if they arise. Finally, we'll step you through the installation process itself, which is a piece of cake. And we won't leave you hanging – once you've booted into Ubuntu for the first time, we'll take you on a tour of the new desktop, reveal how to access existing documents and other files, and show you how to get to grips with your brand new operating system. There's never been a better time to make the life-changing switch to Linux, so grab our hand and take the plunge.

## YOUR COMPLETE GUIDE TO USING WINDOWS!

The best Windows guide money can buy!

## Windows 8.1

## MADE SIMPLE

Enjoy hassle-free computing today with our in-depth advice

148
pages of tips,
tricks and
tutorials

## OUT NOW!
WITH
FREE
DIGITAL
EDITION

FREE
Digital edition of this book!
See page 146 for more information

## DELIVERED DIRECT TO YOUR DOOR

Order online at www.myfavouritemagazines.co.uk
or find us in your nearest supermarket, newsagent or bookstore!

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_31_0.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_31_1.png)

## Back it all up!

Stick with us – before migrating to Linux, make a fail-safe backup.

The simplest way to back up your system is to use the built-in Windows Backup tool in Windows 7 or later – select 'System Image Backup' and follow the prompts. It's not very exciting and it's a little scary, but it is essential. For a pure Linux back-up solution, use SystemRescueCD, which is on the cover disc. Here's how... Reboot your PC with the disc in your drive, access the boot menu if necessary (usually [F11]) and choose your DVD drive, then 'SystemRescueCD'. Problems booting could be caused by your PC's UEFI (see over the page to fix them). Otherwise, pick the default boot options entry. Type uk when prompted for the keyboard layout, and type startx at the final command prompt to access the graphical environment. Once this loads, click the 'Menu' button in the bottom-left and select 'System > Show Filesystems' to identify each partition. The Disk entries identify each physical drive (sda, sdb and so on) and the Device identifies the partitions. In most cases, sda will be your Windows drive, so you'll need to back up sda1 (a small boot partition) and sda2 (the actual Windows partition). You'll also need to note the partition you intend to back up to and make sure it has enough free space. Now switch to the terminal window. To mount the back-up partition, type the following command, changing ntfs to FAT if your back-up drive is FAT32, and replacing sdc2 with the drive's actual partition name:

```
mount -t ntfs /dev/sdc2 /mnt/backup
```

Now re-open the menu and select 'System > Partimage'. This tool lets you back up partitions, so start with /dev/sda1, then press [Tab]. Next, type /mnt/backup/sda1-backup.gz into the 'Image file to create/use' box. Leave 'Save partition into a new image file' selected and press [F5]. Verify 'Gzip' is selected under 'Compression level', then click [F5] again. Enter a description if you wish, then press [Tab] to select 'OK' and hit [Enter]. Make a note about experimental NTFS support, then click 'OK' twice, noting the drive statistics. If this successfully completes, repeat to back up your Windows partition, naming it sda2-backup.gz instead.

To back up your computer's Master Boot Record, open a terminal window and type the following commands

```
cd /mnt/backup
mkdir partition-backup
cd partition-backup
dd if=/dev/sda of=backup-sda.mbr count=1 bs=512
```
to back up MBR. Now back up your partition table with:
```
sfdisk -d /dev/sda > backup-sda.sf
```

If you get a warning about sfdisk not supporting GPT partitions, type sgdisk --backup=backup-sda.sg /dev/sda instead. If disaster strikes, either boot from your Windows rescue disc and follow the prompts, or boot back into SystemRescueCD. If you got as far as Ubuntu resizing your Windows partitions, you'll first need to launch the Gparted partitioning tool from its Taskbar shortcut. It should display your main hard drive (/dev/sda), so identify the extended partition. Right-click each volume inside it and choose 'Delete', then right-click the extended partition and delete that too. Next, right-click your Windows partition and choose 'Resize/Move'. Allocate it all available space, click 'Resize/Move' then 'Apply'. To complete the partition restore process, follow the step-by-step guide (below). The final step is restoring the MBR. Open another terminal window and type:

```
cd /mnt/backup/partition-backup
dd if=backup-sda.mbr of=/dev/sda
```

If you backed up your partition using sfdisk, type sfdisk /dev/sda < backup-sda.sf into the command prompt; if you used sgdisk, type sgdisk --load-backup=backup-sda.sg /dev/sda instead to complete the restore.

## Restore your original setup

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_32_0.png)

### 1 Select backup

Boot into SystemRescueCD as before. Follow the steps in the main text (above) up to identifying your partitions. Next, mount the back-up partition in the /mnt/backup directory. Once done, open Partimage. Leave 'sda1' selected, type the back-up path and name from before into the 'Image file' box.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_32_1.png)

### 2 Restore boot partition

Press [Tab] twice to highlight the asterisk by 'Save partition', then press the down arrow then [Space] to select 'Restore partition from an image file'. Press [F5]. Note the description and press [Enter]. Press [F5] to restore the partition, working through the warnings until the files are copied back.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_32_2.png)

### 3 Restore main partition

Partimage will close once the partition has been restored, so launch it again but this time select your main Windows partition (typically 'sda2'). Then it's a case of repeating the previous steps, only this time using the first back-up file. Note: the restoration relies on your Windows partition being the same size.

## Handling UEFI & Ubuntu

Get your system configured correctly, even Windows 8 systems.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_33_0.png)

Modern PCs, particularly those with Windows 8 pre-installed, have replaced the traditional BIOS with a new system called UEFI. Both perform the same job, detecting and initialising your hardware before handing it over to your OS, but UEFI represents a quantum leap forward from the somewhat primitive capabilities of the traditional BIOS. The UEFI offers a much wider range of features than that found in the BIOS, all wrapped up in a much more user-friendly, graphically pleasing interface.

There are, however, potential issues to circumvent. First, because UEFI is a newer standard, it’s not compatible with legacy hardware. This problem is circumvented by a special Compatibility Support Module (CSM), which enables you to emulate the BIOS to run older hardware and OSes.

More controversially, UEFI also ship with a Secure Boot mode, which, while making PCs less susceptible to malware, were used to lock them to Windows 8. Again, this feature can – in most cases – be disabled, but the good news is that Ubuntu 14.04 LTS fully supports newer hardware and Secure Boot, so you won’t need to disable either to install it alongside

> > “Because UEFI is a newer standard, it’s not compatible with legacy hardware”

Windows. One UEFI feature you’ll need to disable, however, is FastBoot (also called QuickBoot or FastStartup).

### Tweak the UEFI

Accessing the UEFI is the same as entering the BIOS setup. Switch on your PC, then tap the key prompted to enter setup when it appears on-screen (typically [F2] or [Del]). Verify that FastBoot has been disabled by looking for a section called Windows 8 Configuration, or – if it’s not present – Boot. Once located, make sure it’s switched off or disabled.

You may need to tweak the CSM and Secure Boot settings if you intend backing up your system using SystemRescueCD on the cover disc. Again, look in the Windows 8 Configuration, if it exists, for Secure Boot, which may be listed as Windows 8

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_33_1.png)

Make sure your FastBoot settings are disabled before attempting to install Ubuntu.

Logo Requirement. Either way, disable it if you have problems booting SystemRescueCD. If the section isn’t present, look under Security instead.

The CSM module may be part of the Windows 8 Logo Requirement screen, or it’ll be hidden away on its own (we found it buried away at the bottom of the Boot menu on our ASRock motherboard, for instance). Click this to reveal a selection of different options covering different hardware – look for references to PXE (pre-boot environment), GOP (graphics) and Storage (or SATA), as well as USB and PS2, if applicable. This enables you to selectively switch CSM on and off for specific devices as required.

Some motherboards – including our ASRock – enable you to run both modes as required. (In the case of ASRock, we set each one to ‘Do not launch’ to make this setting the norm.) If there’s no apparent options for editing the Secure Boot or CSM settings, contact your PC manufacturer to verify whether or not these can be disabled. In most cases, PCs built using off-the-shelf motherboards should have the required options intact, but some manufacturers have been known to provide hobbled boards.

Upgrading a PC’s graphics card often requires enabling CSM support, so even if the controls aren’t already supported, the manufacturer may have relented under

### Choose the right boot option

Many modern PCs now give you the option of booting either in UEFI or legacy BIOS mode, with the latter mode enabling you to install older operating systems. Ubuntu works fine with both UEFI and Legacy modes, but other environments – including SystemRescueCD – require booting from a legacy option. Some PCs even support mixed-mode booting, presenting both legacy and UEFI choices direct from the boot menu, so you don’t

need to wade into the UEFI shell to switch between them. If you’ve wondered why some boot options are displayed twice in the boot menu, this is why: look more closely and you’ll see one option is prefixed by UEFI. This gives you the option of choosing which mode to boot that drive in, which is a good way of testing whether or not a certain OS or bootable disc works with UEFI or not. If you’re only offered a single set of boot options, your UEFI shell will

only allow you to boot in either UEFI mode or legacy. The latter requires that CSM is enabled, but once done you should be able to change boot settings – including device priority – from within the Boot section of the UEFI shell. If your PC does support mixed-mode booting, you may need to set a different default boot device, in which case take care to select the right mode when choosing which device (typically optical drive or boot hard drive) to make the default.
