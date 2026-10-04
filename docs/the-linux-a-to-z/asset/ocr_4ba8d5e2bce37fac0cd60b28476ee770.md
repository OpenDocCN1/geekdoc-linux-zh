number in the original free inode list should be used as the next start point in the search for more free inodes.

(D) The inode free list has been refilled again from right to left, so that the leftmost inode number will be the last one to allocate and will once again mark the next start point when more free inodes are required.

(E) This scheme works just fine for as long as inodes are being allocated and none are being released. Suppose, now, that inode 72 is released when the file to which it belongs is deleted. With the free inode list in the super block full, there is nowhere to store the newly freed inode number. This is a problem, as we can’t just let inode 72 go free. If we do, it will not be found when we search from inode 182 the next time the super block list needs refilling. In order to make sure that we don’t lose freed inodes in this way, the next inode number in the super block list is replaced by the newly freed lower inode number (inode 72 in the example). This technique ensures that the leftmost inode number in the super block free list is always the correct place to start the next inode array search when looking for more free inode numbers.

(F) No special arrangements need to be made to remember the numbers of inodes that become free when the super block list is already full, if their inode numbers are greater than the next inode number, because they will be automatically found by a linear search starting at next. If an inode is released when there is free space in the super block it can just be added to the super block list.

# 31.2.3 Inode Data Block Pointers

Now that a mechanism exists for allocating a new inode to a file and for finding disk data blocks to add to the file, all that is now required is some method for accessing the data blocks in a file given its inode. The most obvious mechanism for this is to have the data block numbers listed in the inode. Sadly, for any reasonably large file, this solution is impracticable due to the amount of space it would require within the inode.

Looking at the average sizes of files created by typical users shows that the majority are 1024 bytes or less in size and that, as the size of files increases beyond this, the number of files of each size gets less. This suggests that an arrangement which makes accesses to small files quick and efficient, even at the expense of some speed for larger files, would be an acceptable compromise. It is this type of arrangement which System V implements.

Inside a System V inode there is an array of 13 elements, each of which can hold the number of a disk data block (see Figure 31.5). The first ten elements of the array are used to hold the data block numbers of the first ten data blocks assigned to storing the file’s contents.

Assuming, for the purposes of illustration, that each disk data block is 1024 bytes in size, then these ten data block pointers will allow files to be created that are up