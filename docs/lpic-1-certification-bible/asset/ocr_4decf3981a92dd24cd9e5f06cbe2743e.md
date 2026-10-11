# # Checking the File System

+   **Objective**  **2.4  Devices, Linux File Systems, Filesystem Hierarchy Standard**
+   *   Maintain the integrity of file systems. Verify the integrity of filesystems, monitor free space and inodes, fix simple filesystem problems. Includes commands `fsck`, `du`, `df`.

You only need to create a file system occasionally; most people configure their partitions and create file systems only once. The ongoing process is maintaining the file system. Linux provides several useful tools for verifying, monitoring, and fixing file systems. In this section we examine the tools used for these purposes: `fsck`, `du`, and `df`.

# ## fsck

The `fsck` utility is a file system checker utility that is useful for examining file systems to locate and possibly repair problems that are found. When specifying multiple file systems, the checks are run in parallel, unless you use the `-s` option to specify that they should be processed serialized. The `fsck` utility is similar to `mkfs` in that a different utility is used for each file system. Table 5-6 covers the `fsck` utilities and their use.

| Utility | Use |
| :--- | :--- |
| Table 5-6 fsck Utilities | |
| e2fsck or fsck.ext2 | Linux ext2 file system checker |
| dosfsck or fsck.msdos | MS-DOS file system checker |
| fsck.minix | Minix file system checker |


When running these utilities you can use several options to control the actions taken. Table 5-7 shows the options used with the `fsck` utilities.

| Option | Use |
| :--- | :--- |
| Table 5-7 Options Used with fsck | |
| -p | Automatically repairs without prompting. |
| -n | Makes no changes to the file system. |