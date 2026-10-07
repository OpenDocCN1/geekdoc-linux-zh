136 Chapter 5 Startup and Shutdown

other=/dev/hda1
label=msdos

# The Global Section

The first section of the /etc/lilo.conf file applies globally to any kernels that are to be booted from LILO. The first line in the global section shows that LILO is to be installed in the MBR on the first disk, /dev/hda. If LILO were to be the second boot loader, this reference would be to the Linux boot partition, writing LILO here.

The system map in use is /boot/map. This file is a symbolic link to the system map for a kernel that you have created. It is basically made up of debugging information for that kernel. Even Linux system administrators don't usually use this file unless they are doing kernel work.

The next line identifies the boot loader code proper. Typically this is /boot/b . This file contains the code that will reside in LILO's space in the boot sector and the extra LILO relies upon to complete the boot process.

Adding the compact parameter allows LILO to read the hard drive more quickly by transferring sectors at once instead of doing single-sector reads. It works on most modern systems but might cause an other system hang. If so, remove the line.

LILO's default behavior is to wait 4 seconds for you to press the Shift key and boot the default kernel if you do not. The prompt instruction tells LILO to instead prompt the user for which image to boot. This is what causes the lilo: that you have probably seen.

The timeout parameter in the next line sets the time (in tens of a second) to wait for keyboard input. After this period, the default kernel is automatically booted. If you enter the timeout parameter without a numeric value, the timeout period is infinite. During the timeout period, pressing Tab displays a list of available images.

The next line identifies a file containing a message to display before the boot prompt. The message file is limited to 65,535 bytes. Changing or removing the message file requires you to rebuild the file.

If the linear parameter is included, it forces the generation of linear sector addresses instead of the sector/head/cylinder addresses that are used by default. This is necessary if you've configured your BIOS to use any drives in Linear Block Addressing (LBA) mode.

The default parameter sets the default kernel to be booted if no other image label has been given. If no default parameter exists, LILO treats the first kernel specified as the default.