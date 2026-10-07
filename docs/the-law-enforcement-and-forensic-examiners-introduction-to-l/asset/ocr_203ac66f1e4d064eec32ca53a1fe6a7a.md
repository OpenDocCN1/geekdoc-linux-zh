# v.4.33    A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

actual file system blocks that hold the information we are seeking. They are not specific to unallocated data only, but are especially useful for working on unallocated blocks that have been extracted from an image. The tools that manipulate this layer, as you would expect, with **blk** and include:

```
blks
blkcalc
blkstat
blkcat
```

We will be focusing on **blks, blkcalc and blkstat** for the next couple of exercises.

The tool that starts us off is **blks**. This command "lists all the data blocks". If you were to use the -e option, the option would be the same as the output of **dd** for that volume, since -e tells **blks** to "copy every block". However, by default, blks will only copy out the unallocated blocks of an image.

This allows us to separate allocated and unallocated blocks in our file system. We can use logical tools (**find, ls**, etc.) on the "live" file system, and ensure data recovery on only those blocks that may contain deleted or unallocated blocks. Conversely, when we do a physical search of the output of **blks**, we can be sure that artifacts are found from unallocated content.

To illustrate what we are talking about, we'll run the same exercise in TSK Exercise #2A, this time extracting the unallocated data from our volume of interest and comparing the output from the whole volume analysis, just unallocated analysis. So, we will be working on able2.dd. We expect to get the same results in Exercise #2A, but this time by analyzing the unallocated space, and associating the recovered data with its original location in the full disk image.

First we'll need to change into the directory containing our able2.dd. Then we check the partition table and decide which volume we are examining so we know the **-o** (offset) value for our Sleuth Kit commands. To do this, we run the **mmls** command as before:

```
barry@forensic1:-$able2$ mmls able2.dd
dos Partition Table
Offset Sector: 0
Units are in 512-sectors count
```

| Slot | Start | End | Length | Description |
| --- | --- | --- | --- | --- |
| 000: Meta | 0000000000 | 0000000000 | 0000000001 | Primary Table (#0) |
| 001: | 0000000000 | 0000000056 | 0000000057 | Unallocated |
| 002: | 000:000 | 0000000057 | 0000010259 | 0000010203 | Linux (0x83) |
| 003: | 000:001 | 0000010260 | 0000112859 | 0000012600 | Linux (0x83) |

237