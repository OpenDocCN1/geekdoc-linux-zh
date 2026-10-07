```
barry@forensic1:-:/able2$ fsstat -o 10260 able2.dd | less
FILE SYSTEM INFORMATION
```

File System Type: Ext2
Volume Name:
Volume ID: 906e777080e9488d0116064da18c0c4

Last Written at: 2003-08-10 14:50:03 (EDT)
Last Checked at: 1997-02-11 00:20:09 (EST)

Last Mounted at: 1997-02-12 03:22:03 (EST)
Unmounted Improperly
Last mounted on:

Source OS: Linux
Dynamic Structure
InCompat Features: Filetype,
Read Only Compat Features: Sparse Super,

# METADATA INFORMATION

Inode Range: 1 - 12881
Root Directory: 2
Free Inodes: 5807

# CONTENT INFORMATION

Block Range: 0 - 51299
Block Size: 1024
Reserved Blocks Before Block Groups: 1
Free Blocks: 9512

**The fsstat command** provides type specific information about the file system in a volume. As previously noted, we ran **fsstat command** above with the option -o **10260**. This specifies that we get information from the file system residing on the partition that starts at sector offset 10260.

We can get more information using the **fls command**. **fls** lists the file names and directories contained in a file system, or in a directory, if meta-data identifier for a particular directory is passed. The output can be adjusted with a number of options, to include gathering information about deleted files. If you type **fls** on its own, you will see the available options (view the **man** page for a more complete explanation).