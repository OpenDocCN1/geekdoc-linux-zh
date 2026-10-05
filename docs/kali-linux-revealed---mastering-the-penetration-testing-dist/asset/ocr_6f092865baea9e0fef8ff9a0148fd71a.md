Next, the guided partitioning tool offers three partitioning methods, which correspond to differ-ent usages, as shown in Figure 4.10, "Guided Partition Allocation" [page 76].

![](bbox=[0.203, 0.126, 0.796, 0.497])

**Figure 4.10** Guided Partition Allocation

The first method is called "All files in one partition." The entire Linux system tree is stored in a single file system, corresponding to the root (/) directory. This simple and robust partitioning scheme works perfectly well for personal or single-user systems. Despite the name, two partitions will actually be created: the first will have the complete system, the second virtual memory (or "swap").

The second method, "Separate /home/ partition," is similar, but splits the file hierarchy in two: one partition contains the Linux system (/), and the second contains "home directories" (meaning user data, in subdirectories available under /home/). One benefit to this method is that it is easy to preserve the users data if you have to reinstall the system.

The last partitioning method, called "Separate /home, /var, and /tmp partitions," is appropriate for servers and multi-user systems. It divides the file tree into many partitions: in addition to the root (/) and user accounts (/home/) partitions, it also has partitions for server software data (/var/), and temporary files (/tmp/). One benefit to this is that end users cannot lock the system by consuming all available hard drive space (they can only fill up /tmp/ and /home/). At the same time, daemon data (especially logs) can no longer clog the rest of the system.