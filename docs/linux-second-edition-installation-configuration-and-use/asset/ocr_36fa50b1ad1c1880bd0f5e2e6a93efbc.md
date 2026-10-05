# FILE SYSTEM INTERALS 109

+   - Date and time of creation, last read access and deletion of the file.

+   - References to the first 12 data blocks of the file.

+   - Singly, doubly, and triply indirect references to up to 16 million further data blocks (Linux versions running on 32-bit processors, however, limit the size to 2 Gigbytes).

When formatting an ext2 file system by means of the mkfs command, the density of I-nodes can be specified. Normally, one I-node is assigned to every 4 Kbytes (thus, 25000 I-nodes in a partition of 100 Mbytes). In practice this means that only 25000 nodes can be stored in this partition, even if the files are very small and occupy less than 100 Mbytes. If you know that a very large number of small files (or symbolic links) are to be created on a partition, you can choose a greater I-node density (for example, I-node for every 1024 bytes). However, since I-nodes themselves take up space, the available data area of the partition becomes smaller.

# Files

A file consists of an I-node with management information and several data blocks containing the data proper. It is very important that the management information is completely separated from the data and that both can be processed independently. If a file is moved to another directory, only the management information changes, without affecting the data at all.

The number of data blocks required is a function of the file size. One essential piece of information in the I-node is the specification of where (that is, in which data blocks) the data is stored. If the file is bigger than 12 Kbytes, a I-node points to a block directly in the I-node. a block which itself does not contain any data, but references up to 256 data blocks (single level of indirection).

For files that are larger than 268 Kbytes, this is again insufficient: a further I-node value points to a block that points to another 256 blocks of pointers, which finally leads to 256×256 data blocks (double indirection). Now, the maximum file size is 65796 Kbytes. For even bigger files, triply indirect addressing becomes necessary, which allows access to further 256×256×256 data blocks.

# Directories

In principle, directories are managed in the same way as files. From a points of view, imagine a directory as a text file which lists all files and subdirectories by line. Each line contains the name of a file together with its I-node number. Furthermore, this text file contains a reference to itself (..) and a reference to the next higher directory (.). These two cross-references facilitate and accelerate the management of directories.