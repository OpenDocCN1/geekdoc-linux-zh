# Ubuntu and Windows with a Shared Partition

I’d Ubuntu will handle alongside Windows XP, and I want a shared partition so that I can copy files between the two operating systems (Figure C-7). My existing Windows installation was using 7.3GB of the disk because I had files and programs installed on it. I resized the Windows installation to 15GB, leaving 7.7GB of space free for future expansion. Note that the Windows partition will not be formatted, so Windows and all my files on that partition remain intact. I created a 40GB Ubuntu root partition and a 4.2GB swap partition and then created a shared FAT32 partition in the remaining 40GB or so of disk space.

![](bbox=[0.214, 0.267, 0.862, 0.588])

*Figure C-7: Ubuntu, Windows, and a shared partition*

# Finishing Up

When you’ve finished, click **Forward** to finalize your changes. If you’re deleting or formatting any partitions, the changes will be written to disk. This is an irreversible change, so make sure you backed up any valuable data that was on the affected partitions!