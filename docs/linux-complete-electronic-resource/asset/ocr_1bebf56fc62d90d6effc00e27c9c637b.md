The other partitions in the system have to be attached to this root in order for your entire, multiple-partition file system to be accessible. About midway through the boot process, your Unix will make these non-root partitions accessible. It will mount each one onto a directory on the root partition.

For example, if you have a Unix directory called /usr, it is probably a mount point to a partition that contains many programs installed with your Unix but not required during initial boot.

# # How a File Gets Looked Up

Now we can look at a file system from the top down. When you open a file (such as, say, /home/esr/WWW/1dp/fundamentals.sgml) here is what happens.

Your kernel starts at the root of your Unix file system (in the root partition). It looks for a directory there called home. Usually home is a mount point to a large user partition elsewhere, so it will go there. In the top-level directory structure of that user partition, it will look for an entry called esr and extract an i-node number. It will go to that i-node, notice it is a directory structure, and look up WWW. Extracting that i-node, it will go to the corresponding subdirectory and look up 1dp. That will take it to yet another directory i-node. Opening that one, it will find an i-node number for fundamentals.sgml. That i-node is not a directory, but instead holds the list of disk blocks associated with the file.

# # How Things Can Go Wrong

Earlier I hinted that file systems can be fragile things. Now you know that to get to a file you have to hopsotch through what may be an arbitrarily long chain of directory and i-node references. Now suppose your hard disk develops a bad spot?

If you're lucky, it will only trash some file data. If you're unlucky, it could corrupt a directory structure or i-node number and leave an entire subtree of your system hanging in limbo—or, worse, result in a corrupted structure that points multiple ways to the same disk block or i-node. Such corruption can be spread by normal file operations, trashing data that was not in the original bad spot.

Fortunately, as disk hardware has become more reliable, this kind of contingency has become quite uncommon. Still, it means that your Unix will want to integrity-check the file system periodically to make sure nothing is amiss. Modern kinds of Unix do a fast integrity check on each partition at