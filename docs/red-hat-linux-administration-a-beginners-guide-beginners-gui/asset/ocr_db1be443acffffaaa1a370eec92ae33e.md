What this means to you as a system administrator is that the amount of time it takes for the disk to write out data is much less, while the of the same time the safety of getting the data written out to disk quickly means that in the event of a system crash, you won’t need to run **fsck** exhaustively. Even when you do run **fsck**, it only has to check recently modified data, so instead of interminable times, you’ll find that the checks go very quickly.

So which of the four journaling systems should you choose? That call is entirely up to you. But the only one I’ll talk about here is ext3, which is the default file system in Red Hat Linux 8.0.

# Ask the Expert

**Q: Is the ext3 file system the best option for my system?**

**A: I don’t know.**

**Q: Thanks so much. Okay, how does ext3 compare to the other three journaling file systems you mentioned?**

**A: That’s an easier question to answer. Because of its close compatibility with ext2, the ext3 file system lacks some of the features the other journaling file systems implemented because they didn’t have to worry about backward compatibility.**

For example, the largest file you can create in an ext3 file system is 2,048GB. That’s mighty large, but if you expect to need something larger, you may want to consider any of the other three, which can handle files that are orders of magnitude larger. That is, they could do so if the Linux kernel supported file systems larger than 2,048GB, which is not the case with the kernel distributed with Red Hat Linux 8.0.

**Q: Okay, that’s more helpful. What are the relative strengths of the file systems?**

**A: Obviously, ext3 is great from the basis of compatibility. If you already have a Linux partition, you can add journaling functionality to it without pain. If you have a system that uses many small files, ReiserFS (see http://www.namesys.com/) may be just the ticket; it can fit more data onto a partition and handle it much faster than ext2/ext3. If you’re looking for a super-high-capacity file system with very good performance, the XFS file system is your choice. Unfortunately, as I mentioned before, Linux won’t immediately let you take advantage of the storage scale made possible by XFS (see http://oss.sgi.com/projects/xfs/). Your other option, JFS (see http://www-124.ibm.com/jfs/), is less quick with small files than ReiserFS and not as fast with large files as XFS, but it offers good all-around performance. Check out the resources I’ve mentioned here and see what sounds good to you.**