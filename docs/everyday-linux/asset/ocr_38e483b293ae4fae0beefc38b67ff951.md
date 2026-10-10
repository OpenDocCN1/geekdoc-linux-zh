that's compatible with Windows 98, make sure to use FAT32. If you're running Windows 95 or lower, you should use FAT16.

# ## The Drive Summary

The drive summary contains information about the physical hard drives presently installed on your computer. It will list them in order, hda first, hdb second, and so on. You will notice in this list that you can skip letters, so hdd may follow hdb or even hda. The drive summary is under the partition summary. There are several categories that you should understand here, too.

+   - **Drive Geometry** This information is fairly technical and relatively unimportant to your understanding of the installation. The drive geometry determines how much space is allocated for your hard drive. The drive geometry is composed of cylinders, heads, and sectors.

+   - **Total** The total category tells you how much information your hard drive can hold in megabytes.

+   - **Used** The used category tells you how much of the total space your partitions are taking up.

+   - **Free** The free category is simply the difference between the total and the used space. You should use this category to decide how much space to allocate for partitions.

# ### Working with the Partitions

Directly below the partition summary is a group of buttons. One says “add,” another “delete,” and yet another “edit.” In the course of working with the partitions, you're going to be deleting some partitions, adding others, and so on and so forth. These are the buttons that we use to accomplish these tasks.

Your first task is to identify which hard drive you're going to install Linux on. If you plan on dual booting using two hard drives, you'll probably be installing it on either hcb or hdd—the primary slave hard drive or the secondary slave hard drive. If you do not plan on dual booting or if you plan on dual booting on a single drive, you'll use the drive labeled hda. Preparing for each of the three procedures is described below.