chapter using the GRUB2 bootloader, as it is used in a majority of Linux distributions. A few Linux distributions still use old software for the boot and startup process, but we will not be going through them.

# The Boot Sequence

The boot sequence can be initiated in a couple of ways for Linux. The simplest one is turning on the power for your Linux system. If there is a user created on the system or logged in as a root user, you can initiate a reboot of the system via the command line to trigger the boot sequence.

# BIOS POST

The first step of the boot sequence in Linux is not related to Linux and its operations. The first step is all about initiating the hardware on the system and is common across all operating systems. When you press the power button for your system, a test known as the Power On Self Test or POST is short is initiated. POST is a part of the Basic Input Output System or BIOS.

BIOS was introduced for the first time in 1981 when IBM developed its first computer. POST is a module of BIOS that is in place to check if all the hardware on the system is functional. IF POST fails, it indicates that there is something wrong with the system. The system will be in an unusable state, and BIOS would not be initiated.

POST and BIOS’s function is to check if all the hardware needed to start the system is functional. They also follow up with a BIOS interrupt known as INT 13H, which is responsible for finding bootable devices such as a hard disk and initiating it by locating its boot sectors. When the interrupt locates the first boot sector containing a valid boot record, it is loaded into the memory and the control gets transferred to the code present in the boot sector.

You can say that the boot sector is the first stage of the boot loader. There have been around three bootloaders that have been used across Linux distributions over the years, LILO, GRUB, and GRUB2. The latest and most popular bootloader is GRUB2, and every latest Linux distribution now uses GRUB2.