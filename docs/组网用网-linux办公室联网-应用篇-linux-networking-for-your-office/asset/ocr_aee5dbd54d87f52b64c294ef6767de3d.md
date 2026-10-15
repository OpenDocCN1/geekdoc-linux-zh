# NOTE

The word filesystem has two meanings in Linux. One is the low-level layout of data on a partition or removable medium. This is the meaning of the word used earlier in this chapter, when referring to ext2, FAT, HFS, and other filesystems supported by Linux. The second meaning of the word, and the one that applies to the previous paragraph, is the high-level logical layout of data on the system—that is, how directories and files are organized in relation to one another. This sense of the word refers to what you would type at a command prompt or in a file open dialog box to access a file. In general, which meaning of the word is relevant should be apparent from context. Where there might be ambiguity, I’ve tried to clarify it by making the meaning explicit or by using terms such as partition or directory structure when they’re appropriate.

# Partitions and Mount Points

Linux, like UNIX, uses a filesystem structure that’s substantially different from that of DOS, Windows, OS/2, or MacOS. In all these desktop OSs, you access each partition or removable disk via an identifying label, such as C: or MyFiles:. Under Linux, there are no drive letters or partition labels. Instead, the first partition, known as the root partition, or /, serves as a base on which all others stand. Files and directories can exist in the root partition, and you can access them by preceding their names by /, as in /test-file.txt or /test-directory/. You mount additional partitions at mount points—empty directories—on the root partition. Thereafter, everything under the directory that serves as a mount point resides on the mounted partition. One exception to this rule is that you can mount a partition under a secondary partition, and so on. Figure 9.1 illustrates this relationship. Note that precisely which parts of the filesystem structure exist as separate partitions is arbitrary, and is determined when you install Linux or in subsequent system reconfigurations.

![](bbox=[0.24, 0.82, 0.65, 0.95])

# FIGURE 9.1

To the user, it’s irrelevant that /home is on a separate partition from /; the partitions are all part of a unified tree.