v.4.33                               A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

004: 000:002   0000112860   0000178694   0000065835 Linux Swap / Solaris x86
(0x82)
005: 000:003   0000178695   0000675449   0000496755 Linux (0x83)

As Exercise #2, we've decided to search for the unallocated space in the second Linux partition (at offset 10260, in bold above).

We run the blkls command using the offset option -o which indicates what partition's file system we are exporting the unallocated space. We then redirect the output to a new file that will contain only the unallocated blocks of particular volume.

```
barry@forensic1:~/ blkls -o 10260 able2.dd > able2.blkls
```

```
barry@forensic1:~/ ls -lh able2.blkls
-rw-r--r-- 1 barry users 9.3M May 28 14:44 able2.blkls
```

In the command, we are using blkls on the second partition (-o 10260) within the able2.dd image, redirecting the output to a file called able2.blkls. The file able2.blkls will contain only the unallocated blocks from the target file system. In this case we end up with a file that is 9.3M in size.

Now, as we did in our previous analysis of this file system (Exercise #2) we will use grep, this time on the extracted unallocated space, able2.blkls file, to search for our text string of interest. Read through Exercise #2 if you need a refresher for these commands.

```
barry@forensic1:~/ grep -abi cybernetic able2.blkls
1631299: updated by Cybernetic for linux rootkit
9317041:Cybernetic proudly presents...
9323055:Email:cybernetic@nym.alias.net
9323087:Finger:cybernetic@nym.alias.net
```

The grep command now tells us that we have found the string cybernetic at four different offsets in the extracted unallocated space. We will concentrate on the first hit. Of course these are different from the offsets we found in Exercise #2 because we are no longer searching for the original image.

The next obvious question is “so what?”. We found evidence in our extracted unallocated space. But how does it relate to the original image? As forensic examiners, merely finding potential evidence is not good enough. We also need to know where it came from (physical location in the original image), what it belongs to or (possibly)

238