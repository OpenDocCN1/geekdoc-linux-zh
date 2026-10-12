In order for a requested sector to be read, the armature must first seek to the proper track. Once it is at the correct track, the disk must wait for the requested sector to rotate under the head. The time it takes for the drive to seek is called the seek time. The time it takes for the data to rotate under the head is known as rotational latency. Seek time and rotational latency are shown in Figure 4-6. Later in this section, both of these concepts will be covered in greater detail.

A typical disk drive is made up of more than one platter and both sides of the platter are used. These platters are stacked on top of each other and have multiple heads connected to a single armature. Since all of the heads are stacked on top of each other and can read and/or write simultaneously, it is more efficient to do this. Thus, a disk drive will read and/or write multiple sectors simultaneously. Remember that both sides of the platter are used.

The stack of tracks used to store data is called a cylinder. By allowing all of the heads to be used at once, a disk drive can access and write data much faster than moving to each sector individually. Disk cylinders are shown in Figure 4-7.

In order to understand the performance of a disk drive, you must understand the performance of seeks and rotational latency.

# **Seek Time**

A seek is the motion of the disk armature to move from one track to another, and the seek time is the time it takes for the armature to move from one track to another. Seeks can be divided into three different types: full disk seeks, track-to-track seeks, and random seeks. Although functionally the same, they are categorized separately due to the different performance characteristics.

![](bbox=[0.15, 0.59, 0.85, 0.84])

**FIGURE 4-6.  Seek time and rotational latency**