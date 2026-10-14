# Appendix B: An Introduction to Disk Partitions

noting that there is no single, universal filesystem; as Figure B-3 shows, a disk drive may have one of many different filesystems written on it. As you might guess, different filesystems tend to be incompatible; that is, an operating system that supports one filesystem (or a handful of related filesystem types) may not support another. This last statement is not a hard-and-fast rule, however. For example, Red Hat Linux supports a wide variety of filesystems (including many commonly used by other operating systems), making data interchange easy.

![](bbox=[0.52, 0.35, 0.68, 0.62])

# Figure B-3: Disk Drive with a Different Filesystem

Of course, writing a filesystem to disk is only the beginning. The goal of this process is to actually store and retrieve data. Let’s take a look at our drive after some files have been written to it.