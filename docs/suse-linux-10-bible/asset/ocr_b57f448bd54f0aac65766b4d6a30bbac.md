The benchmarks represented in the graph are as follows:

+   1. Untar the kernel 2.4.26 kernel. This represents a large amount of small files being created on the filesystem.

+   2. Tar the same source tree. This shows a large amount of small files being queried and read.

+   3. Remove the kernel source tree. This represents a large amount of files being removed from the filesystem.

+   4. Copy the kernel tarball ten times. This represents the reading of a large file many times over and shows filesystem performance and the performance of the read-ahead buffer.

+   5. Create a 1GB file. This shows how well the filesystem handles the creation of a large file. This is especially good at showing how well the filesystem deals with allocating a large amount of space over a large disk.

+   6. Copy a 1GB file. This represents how well the filesystem deals with both reading and writing a large file. This is valuable for fileservers that have to deal with large files.

+   7. Stream data from a 1GB file to the null device. The null device is a black hole that is able to read any data and drop it immediately. This represents how well the filesystem can read a file.

As you can see in the benchmarks, ReiserFS is very good at dealing with small file operations, whereas EXT2 is good at reading large files. XFS copies files sequentially well (not as well as EXT2), whereas JFS proves the best at reading the 1GB file.

These tests are no means conclusive, but they are here to give you an idea of how well the filesystems perform. Choosing one is a matter of judging how data is manipulated on your system and how you see changing in the future. For general information about the capabilities and design of each of the types of filesystems shown in Figure 3-2, see the section that introduces the filesystem earlier in this chapter.

# Mounting Filesystems

After a filesystem has been created, you will probably want to use it. The process is different from that of other operating systems, such as Windows, where all filesystems are automatically loaded. In Unix, a filesystem has to be mounted by the operating system. Mounting is the process where the root of the filesystem is attached to your system's file hierarchy by associating it with a directory. This may seem like an archaic way of accessing your data, but it does provide you with a transparent way of accessing all the data (local and remote) under a single administrative domain.