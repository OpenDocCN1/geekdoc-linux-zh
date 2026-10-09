$ df /usr

Filesystem 1k-blocks Used Avail Capacity Mounted on
/dev/ad0s1g 3408662 988696 2147274 32% /usr

The reported number of 1k-blocks, 3408662, equates to the number of 2k-blocks that our `print_statvfs` program showed, 1704331.

There’s also a standard way to read the information in an i-node, so you don’t have to read the device file as we did in the previous section. We’ll get to that in Section 3.5.

# **3.2.4 Mounting and Unmounting File Systems**

A UNIX system can have lots of disk file systems (hard disks, floppies, CD-ROMs, DVDs, etc.), but they’re all accessible within a single directory tree that starts at the root. Connecting a file system to the existing hierarchy is called *mounting*, and disconnecting it *unmounting*. Figure 3.1 shows a large file system that contains the root (i-node 2, with directory entries x and y) and a smaller unconnected file system, with its own root, also numbered 2. (Recall that 2 is always the i-number for a root directory.)

![](bbox=[0.22, 0.54, 0.78, 0.775])

**Figure 3.1** Two disconnected file systems.