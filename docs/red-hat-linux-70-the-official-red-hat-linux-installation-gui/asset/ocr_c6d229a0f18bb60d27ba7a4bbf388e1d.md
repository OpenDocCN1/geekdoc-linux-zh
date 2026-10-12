Recommended if you are already using another boot loader on your system (such as OS/2's Boot Manager). In this case, your other boot loader will take control first. You can then configure that boot loader to start LILO (which will then boot Red Hat Linux).

# Figure A–5 LILO Configuration

![](bbox=[0.12, 0.28, 0.7, 0.6])

If you choose to install LILO, please select where you would like LILO to be installed on your system (see Figure A–5, *LILO Configuration*). If your system will use only Red Hat Linux you should choose the master boot record (MBR). For systems with Win95/98, you also should install LILO to the MBR so that LILO can boot both operating systems.

If you have Windows NT (and you want to install LILO) you should choose to install LILO on the first sector of the root partition, not the MBR. Please be sure to create a boot disk. In a case such as this, you will either need to use the boot disk, or configure the NT system loader to boot LILO from the first sector of the root partition. Be sure to check out <http://www.linuxdoc.org/HOWTO/mini/Linux+NT-Loader.html> for more information on setting up LILO and NT.