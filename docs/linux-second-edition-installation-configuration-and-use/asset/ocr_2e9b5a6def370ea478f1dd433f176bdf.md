# CONFIGURATION AND ADMINISTRATION

If you first install LILO and then Windows 9x (or another operating system), LILO is overwritten without warning. It is easy to reinstall LILO by calling LILO under Linux. However, you need a boot diskette to be able to start Linux at all. Therefore, do not throw away Linux boot diskette after a successful LILO installation!

Also, if you update your Linux system (new kernel), please do not forget to update your boot diskette as well.

# Functioning

To put it simply, the function of LILO is to load and execute the file containing the Linux kernel. However, this is not as easy as it sounds:

More precisely speaking, the boot sector of the hard disk or diskette contains a tiny program (first stage), whose only task is to load the larger LILO main program (second stage). The boot sector, that is, the first of the hard disk or diskette, would be much too small to store the entire LILO program. Code contained in the boot sector is automatically executed by the BIOS at start-up – this is why the boot sector plays such an important role in starting a computer.

The LILO main program (the file /boot/boot.b) is located anywhere on the hard disk. The boot sector with the start program also contains the numbers of the sectors where the main program can be found.

As soon as the LILO main program is running, it gives the user the possibility to choose between different operating systems via the keyboard. If the user opts for Linux, LILO must load the kernel file. For this purpose, a table was created during installation of LILO (the file /boot/map), which contains the sequence of all sectors in which the kernel file is located.

The reason for this unusual procedure is that while LILO is running, no-information is as is available on DOS, Linux, or other files. From Linux's point of view, the hard disk is a huge conglomerate of data sectors. LILO must know at each stage where the data sectors are that needed.

On the basis of the above description, it should be clear that LILO can only function as the location of the kernel file on the hard disk remains exactly the same. (Each copy command and, in particular, recompilation of the kernel causes a change even if the file name remains the same. In such cases, LILO needs to be reinstalled by the LILO command. LILO carries out the preparatory work, creating updated versions of /boot/boot.b and /boot/map, and storing them all sectors and other information in the boot sector).

LILO is executed before any operating system is running. For this reason unlike Linux – LILO has to rely on the BIOS. For historical reasons, however, the BIOS only allows access to the first 1024 cylinders of a hard disk. In order to make the startup of Linux work, the kernel file must be located within the first 1024 cylinders of the hard disk. With older BIOS versions or hard disks, the location of the Linux kernel may be limited to the first 508 Mbytes of the hard disk. Depending on