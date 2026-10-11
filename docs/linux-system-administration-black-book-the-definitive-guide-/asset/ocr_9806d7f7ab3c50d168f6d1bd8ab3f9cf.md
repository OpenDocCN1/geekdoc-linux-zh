# In Depth

The file system is a combination of the partitions and directories that make up your Linux system, plus or minus any devices you add and remove along the way. It is important to keep the file system healthy and organized or you end up spending more time searching for files and programs than actually administering the system. When the file system does eventually fail—which will happen on a machine that is used over a long period of time—how you have managed this system and prepared for this problem determines how traumatic the experience is.

# Hard Drive Overview

First, it is important to understand the overall structure and terminology used in this chapter, although you should already understand the basics of breaking down drives for installation and moving around a file system. As with other operating systems, the Linux kernel plus the files associated with it are stored on a hard drive, which is a physical unit. Within each hard drive are partitions, which function somewhat as virtual hard drives. Then, inside each partition, you build a file system.

# Behind The Scenes

Linux uses the *second extended (ext2)* file system, which was created specially for use with this operating system. This file system is not relegated to hard drives, but is placed on any media that you use to store Linux data. Understanding how the file system is broken down is helpful when you are trying to figure out file system manipulation commands.

# Data Storage Layout In ext2

Data within the ext2 file system is stored in a series of identically sized data blocks, as shown in Figure 3.1. These blocks are generally 1,024 bytes, though you can set them to be a different size while making a file system. Whether a file is 10 bytes or 1,020 bytes, it takes up one data block, which cannot be used to store anything else. Those files larger than 1,024 bytes, whether they are 1,025 or 2,026 bytes, take up two data blocks. Due to the nature of file systems with files continuously being added and deleted, these blocks may or may not be physically next to one another.