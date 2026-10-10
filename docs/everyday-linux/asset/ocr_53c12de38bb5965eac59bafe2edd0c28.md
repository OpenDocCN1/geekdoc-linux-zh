# ## **Editing Partitions**

If you have two hard drives, one of which is another format, you can also specify a mount point for that drive and Linux will automatically mount the drive when you boot up the computer. To specify a mount point, you must highlight the partition in question and then click the edit button.

The only information you will be able to change within this dialogue box is the mount point. You can specify basically any mount point that you wish, but the naming convention is a little different.

In Windows systems, each different directory in the directory tree is separated by a backward slash (\) when called by its *absolute pathname*. The absolute pathname is, for all intents and purposes, the full name of the directory or folder. In Windows, for instance, much attention is paid to the System folder, but its absolute pathname is C:\Windows\System.

In Linux, folders are called directories and they are separated from one another by using a forward slash (/).

When you name a mount point, you are specifying a directory where Linux will store the files in the partition. Each of the mount points will begin with a forward slash and then a combination of directories. Most hard drives are *mounted* in the /mnt directory, so if you have a hard drive with Windows on it, you could use a mount point of /mnt/windows. Alternatively, you could use /what-chama-cali or any other mount point you desire as long as it fits the naming convention specified by Linux.

# ## **Selecting Partitions to Format**

In the event that you are using a custom installation, you will be able to specify which partitions you want to format during the installation of packages. Initially, you should select all of them—only Linux-type partitions are listed, so you won't endanger files anywhere else. Make sure that you also check the option, “Check for bad blocks during format.” This will take a little extra time, but it gives you the added benefit of ensuring that the drive is suitable to carry data.

If you’re installing Linux for the second time, or using the upgrade option from the installation to upgrade to a new version of Linux, you should not specify those partitions on which you want to save data, such as the /usr/local partition. Make sure you have your list of partitions handy.