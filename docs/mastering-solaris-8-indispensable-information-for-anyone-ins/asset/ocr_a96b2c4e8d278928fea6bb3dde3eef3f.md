# FIGURE 2.11

Two processes mapped
to the same file

![](bbox=[0.32, 0.13, 0.78, 0.63])

# Anonymous Memory

Anonymous memory pertains to pages that are not associated with a vnode. These pages are used for heap space, a stack, and copy-on-write pages. Two subsystems are dedicated to managing anonymous memory. The first is the anon layer, the second is the swapfs file system. When a segment receives a page fault, it allocates an anon map structure and points to the anon header in the amp field on the anonymous map. A slot array is then allocated. It is big enough to hold the number of pages in the segment. Depending upon how many slots are required, the slot array may be a single or double indirection list.

Double indirection is indicated when segments are larger than 16MB; 32-bit systems fall into this category, as do 64-bit systems for segments larger than 8MB. For single indirection, the anon header array-chunk directly references the anon slot array. For