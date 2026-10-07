SCSI Device: External lomega Zip—100 drive

Sound card: Integrated motherboard VIA 82c686a sound chipset

If you've purchased a Red Hat Official boxed set, it will include the image to create a boot diskette that supports a CD-ROM installation like the one we'll perform. If your computer supports booting from a CD-ROM, you can boot directly from the Red Hat CD-ROM and will not need to create a boot disk. If it does not, or if you are installing from a different medium, you might have to create your own boot disk as described later in this chapter.

# Choosing a Partitioning Scheme

Disk partitioning is the division of the hard drive into logical parts that contain specific components of the operating system.

Although most people choose a more structured file system layout, Red Hat 7.3 requires only one Linux partition. Assuming its size is sufficient, this partition can contain both the root partition and all the other directories that fall beneath. An advantage of this simplistic approach is that you don't have to guess how large each filesystem will eventually grow to be. A disadvantage is that you cannot set quotas for individual directory structures and you cannot mount any of the directories under the root partition as read-only, since that requires the directory to live on its own partition. More important still is the fact that dynamic data as exists within the `/home` directory coexisting with the root filesystem is generally a bad idea, since corruption can cause the entire system to become unstable and possibly even unable to boot at all.

In a more structured approach, you might find that you've set aside too little space for a partition and need to find more space. There are several options for adding space:

+   Back up and reinstall, enlarging the partition in question.
Add a new drive to the system and move some of the data from the bloated partition to the new one.
Move some of the data from the bloated partition to another existing partition.
Create a symbolic link so that users will find the data where they expect it to be.

Note Just as there are "distro wars", there are also partitioning scheme wars. Linux users have long argued about the optimum scheme, and there is no sign that they will stop. One of the premier features of Linux, after all, is the freedom to disagree.

Red Hat has simplified the situation for new users by setting up installation classes. These classes select a partitioning scheme and software packages appropriate to the chosen use. In each case, you have the option of overriding that class's standard partitioning scheme and package selection. There are four established installation classes: the Workstation-Class, the Server-Class, the Laptop-Class, and the Custom-Class. In this case, we'll be performing a Server-Class installation. The others are listed below for completeness.

# Workstation-Class Installation

Use the workstation-class installation on an end-user desktop system. A system installed in this way is not intended to act as a server, but it does set up the X Window System environment.

A workstation-class installation requires at least 850MB of free disk space. If your hard drive already contains partitions of other types, like Windows, the workstation-class installation will

41