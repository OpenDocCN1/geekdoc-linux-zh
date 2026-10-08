# ## Using the df Utility

The df utility reports the number of 1024-byte blocks that are allocated, used, and available; the percentage used; and the mount point. The reports displayed are based on the command options entered.

+   1. To use the df command to check hard disk usage:
2. Type **df** and then press **Enter**. (Note that you can enter the df utility without options.) Your screen looks similar to Figure 8-6.

![](bbox=[0.21, 0.3, 0.78, 0.63])

Figure 8-6: Output of df command

Of course, your file systems and their statistics will differ from those shown in Figure 8-6. In Figure 8-6, the df command reports that the /dev/hda5 file system has 9,376,851 blocks of 1 kilobyte each. There are 910,280 blocks in use; and 7,980,087 blocks available. Ten percent of the blocks are in use, and the file system is mounted on /.

+   2. You may specify a file system as an argument. The statistics for that file system alone appear on the screen. Type **df /dev/hda1** and press **Enter**. You see the disk statistics for the /dev/hda1 file system. Figure 8-7 shows an example.