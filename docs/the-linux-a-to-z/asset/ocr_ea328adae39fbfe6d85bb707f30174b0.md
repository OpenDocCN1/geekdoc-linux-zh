![](bbox=[0.12, 0.07, 0.88, 0.22])

![](bbox=[0.12, 0.24, 0.88, 0.38])

![](bbox=[0.12, 0.39, 0.88, 0.53])

![](bbox=[0.12, 0.54, 0.88, 0.68])

![](bbox=[0.12, 0.67, 0.88, 0.81])

![](bbox=[0.12, 0.79, 0.88, 0.93])

# Figure 31.4 Allocation and release of free inodes.

request is made. The inode numbers which appear in the list were discovered on a linear search of the inode array. During the search, the super block list is filled from right to left (in the diagram) so that the leftmost inode number in the list is the largest free inode so far discovered.

(B) Here two inodes have been allocated (I-40 and I-41) and the index has been moved accordingly.

(C) After several more inode numbers have been allocated, the super block free list eventually gets to its last entry. When this inode is allocated, a new search is made through the inode array to find more free inode numbers with which to refill the super block list. However, there is no point in searching the inode array from the beginning because we already know that all the inodes up to 100 (in our example) are already in use. This suggests that the leftmost inode