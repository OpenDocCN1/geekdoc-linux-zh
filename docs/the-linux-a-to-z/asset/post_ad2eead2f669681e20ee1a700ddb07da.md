
A good tip at this point is to make a note of the numbers of blocks in the Linux partitions for later operations (16640 and 147200 here). Using the 'w' command we will now write this new partition table back to the disk and then quit from fdisk. While using fdisk, if something should go horribly wrong, you can use the 'q' command to quit from the program without making any changes to the original partition table on disk.

To make sure that the changes to the partition table take effect with all versions of fdisk you should now reboot the machine with the boot and root disks again. Once you have done this and logged back in as root again, you are ready to continue.

## 7.3.2 Creating Filesystems

Having now created the partitions for Linux, the next task is to make the filesystem structures within those partitions. This is just the Linux equivalent of the DOS format operation. Working on the swap partition first, you use two commands: mkswap to prepare the partition and swapon to tell Linux to bring the partition into use:

```
# mkswap -c /dev/hda2 16640
# swapon /dev/hda2
```

The -c switch to mkswap forces a check for bad data blocks in the partition. Obviously, if your swap partition is not hda2, then you would substitute the name of yours in the command. The number at the end of the line is just the block count of the swap partition, which you noted when you created the partitions. Again, you will substitute your own value in place of the 16640. The swapon command just takes a single parameter which is the name of the partition to use (hda2 here).

Before you can create the filesystems on the Linux native partitions, you have to choose which filesystem type to use. In fact, even though Linux supports several different filesystem structures, the best one all round is called the Second Extended Filesystem and it is the one to use. To make a second extended filesystem on a Linux native partition you use the mke2fs command:

```
# mke2fs -c /dev/hda3 147200
```

The parameters specify the partition to use and its size in blocks. Again, the -c switch forces a bad block check. If you have more than one Linux native partition then you will need to use mke2fs on each of them.

## 7.3.3 Installing Packages

Having prepared the disk partitions, you are now ready to load the Linux software into them. Each different Linux distribution has a different method for performing
this operation. But essentially what happens is that your Linux partitions are mounted under the root filesystem (which is still in RAM, don't forget) and then the various software packages can be unpacked from floppy disk (or other installation medium) and copied into the appropriate places.

Some distributions require you to perform these operations manually, which is not a particularly difficult task, just a bit tedious. Other distributions, Slackware included, provide an installation script to automate the procedure. The installation script in the Slackware distribution is called setup:

```
# setup
```

Running this command presents you with a menu which will guide you through the remaining steps of the installation. The various menu options are:

- help Displays the setup help file.
- keymap Allows you to change the keyboard mapping if you have a non-US keyboard. This will be the first option to choose to start the installation proper for non-US keyboard users. When you finish with this option setup allows you to move directly to the addswap option without coming back to the main menu.
- quick Here, you select between quick and verbose installation. As a beginner you should probably use the verbose option, which is the default anyway.
- make tags When you gain more expertise with Slackware installation, this option allows you to set up your own tag files to pre-select which software packages to use out of each disk set.
- addswap Allows you to specify which of the Linux swap partitions you want your final system to use as swap space. I have already said that it is possible to create and use more than one swap partition, but why you wouldn't want to use all of them automatically I can't imagine. Anyway, this information will be incorporated later into one of the system configuration files.

After making your selections you will be asked if you want to run mkswap and swapon on these partitions. If you have already used these commands on the partitions before running setup (which we did) then you should choose not to allow setup to do it now.

This menu option will be the first to choose to start the installation proper, if you have a US keyboard. When you finish with this option, setup allows you to go on to the next step rather than return to the main menu.

- target This is where you specify which of your disk partitions you wish to include in your final directory hierarchy. A list of the available partitions is given and you are asked which to use as the root filesystem. In our example there is only one to choose from – /dev/hda3. If you haven't already done so (we did) you can now create the filesystem on the root partition with mke2fs. If applicable, you will then be asked if there are any other partitions you want to use and upon which directories you would like to have their filesystems mounted. This is where you would specify the /home partition, for example if we were dealing with the partition layout of Figure 7.2.

- **source** This is where you specify the source medium from which the installation will take place. Generally the choices are: CD-ROM, floppy disk, hard disk or network. If you choose floppy disk here, then a further menu will allow you to specify which floppy drive to use and the size of disks that fit the drive. In fact, whichever option you choose, further questions may be used to determine exactly where the source files will come from.
- **disk sets** This option allows you to choose which disk sets you want to install. You must install the A set. Beyond that, the choice is yours. You will end up with a fairly full and general usage installation if you include the following: A, AP, D, K, N, F, X, XAP and Y.
- **install** This is the menu option which actually unpacks the packages you select for installation and copies their files into your Linux filesystems. Normally, you will arrive at this option directly from the previous option, rather than from the main menu.

You will now be asked how you wish to be prompted and, as a beginner, you should answer by selecting the *normal* option.

Each disk set contains a list of packages. Some of these packages are tagged as REQUIRED and these will be installed automatically, if you choose to install the disk set to which they belong. Other packages within each disk set are tagged as RECOMMENDED or OPTIONAL and in these cases you will be asked whether or not you wish to install them. You should make sure that you read all the on screen information carefully during the installation procedure as, sometimes, you need to make a choice between packages and not just install them all.

- **configure** After the package installation has taken place, this option allows you to set up the mechanism for booting Linux either from floppy disk or hard disk and it also allows you to perform some machine configuration for such things as: mice, modems and networks. Initially, you are probably better skipping some of the configuration options and performing them manually when you have had the chance to look at what is involved. However, you should take the opportunity to create a boot floppy at this time, and perhaps configure lilo (see Section 7.3.6 for information to help you with lilo).
- **pkgtool** This option is only provided for use later, for package maintenance. It will allow individual packages to be added and deleted. The use of this option is quite self-explanatory.
- **exit** Leave setup and return to the shell prompt.

## 7.3.4 Booting Linux

Whatever Linux distribution you choose to install, it must provide you with some means of booting into Linux when you first switch the machine on. This can be as simple as supplying you with a floppy disk to boot from or you may get to use one of the Linux kernel loaders from your hard disk. The Slackware distribution allows
