**source** This is where you specify the source medium from which the installation will take place. Generally the choices are: CD-ROM, floppy disk, hard disk or network. If you choose floppy disk here, then a further menu will allow you to specify which floppy drive to use and the size of disks that fit the drive. In fact, whichever option you choose, further questions may be used to determine exactly where the source files will come from.

**disk sets** This option allows you to choose which disk sets you want to install. You must install the A set. Beyond that, the choice is yours. You will end up with a fairly full and general usage installation if you include the following: A, AP, D, K, N, F, X, XAP and Y.

**install** This is the menu option which actually unpacks the packages you select for installation and copies their files into your Linux filesystems. Normally, you will arrive at this option directly from the previous option, rather than from the main menu.

You will now be asked how you wish to be prompted and, as a beginner, you should answer by selecting the *normal* option.

Each disk set contains a list of packages. Some of these packages are tagged as REQUIRED and these will be installed automatically, if you choose to install the disk set to which they belong. Other packages within each disk set are tagged as RECOMMENDED or OPTIONAL and in these cases you will be asked whether or not you wish to install them. You should make sure that you read all the on screen information carefully during the installation procedure as, sometimes, you need to make a choice between packages and not just install them all.

**configure** After the package installation has taken place, this option allows you to set up the mechanism for booting Linux either from floppy disk or hard disk and it also allows you to perform some machine configuration for such things as: mice, modems and networks. Initially, you are probably better skipping some of the configuration options and performing them manually when you have had the chance to look at what is involved. However, you should take the opportunity to create a boot floppy at this time, and perhaps configure lilo (see Section 7.3.6 for information to help you with lilo).

**pkgtool** This option is only provided for use later, for package maintenance. It will allow individual packages to be added and deleted. The use of this option is quite self-explanatory.

**exit** Leave setup and return to the shell prompt.

# 7.3.4 Booting Linux

Whatever Linux distribution you choose to install, it must provide you with some means of booting into Linux when you first switch the machine on. This can be as simple as supplying you with a floppy disk to boot from or you may get to use one of the Linux kernel loaders from your hard disk. The Slackware distribution allows