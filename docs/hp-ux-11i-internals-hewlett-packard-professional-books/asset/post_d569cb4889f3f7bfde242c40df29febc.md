
![](img/08b7d2492fc1415a694a5fb16a8fdeb3_201_0.png)

Figure 6-10 The b-tree

The base of the tree is its **broot**. It sets the rules for the tree's usage and directs us to the first level **bnode** in the tree. This first **bnode** is sometimes called the root **bnode** — try not to confuse the two structure names.

The **bnode** structures are ranked and ordered according to the tree's depth (defined in the **broot**) and form the tree's **branches**. To continue with the tree model, the **chunk** structures could be thought of as the leaves on the branches. Each chunk contains **vfd** | **dbd** structure pairs; these **vfd** | **dbds** are the fruit of a successful search of the tree.

## Broot, Bnodes, and Chunks

Let's examine the b-tree structures in Listings 6.9 and 6.10.

Listing 6.9 q4> fields struct broot

```
We start off with a pointer to the root (first) bnode and
record the depth of the b-tree
0 0 4 0 * b_root
4 0 4 0 int b_depth
Next we find the number of pages mapped and the number of swap
pages reserved for this tree
8 0 4 0 int b_npages
12 0 4 0 int b_rpages
The page list pointer directs us to this region's page list,
and nfrag points to the next available chunk (required if we
need to grow the tree)
16 0 4 0 * b_list
20 0 4 0 int b_nfrag

This pointer gets us back to the region structure this b-tree serves
24 0 4 0 * b_rp
28 0 4 0 int b_protoidx

There are two sets of prototype dbd structures when the b-tree is being initialized or grown; the protoidx gives an index into the tree where we switch from using the first prototype to the second
32 0 3 u_int b_proto1.dbd_type
32 3 3 u_int b_proto1.dbd_data
36 0 3 u_int b_proto2.dbd_type
36 3 3 u_int b_proto2.dbd_data

This array stores information about ranges of pages that need to have their copy-on-write bit set
40 0 4 0 int b_vproto.v_start[0]
44 0 4 0 int b_vproto.v_start[1]
48 0 4 0 int b_vproto.v_start[2]
52 0 4 0 int b_vproto.v_start[3]
56 0 4 0 int b_vproto.v_start[4]
60 0 4 0 int b_vproto.v_end[0]
64 0 4 0 int b_vproto.v_end[1]
68 0 4 0 int b_vproto.v_end[2]
72 0 4 0 int b_vproto.v_end[3]
76 0 4 0 int b_vproto.v_end[4]

To speed up repetitive references, the two most recent key/value data pairs are cached here
80 0 4 0 int b_key_cache[0]
84 0 4 0 int b_key_cache[1]
88 0 4 0 * b_val_cache[0]
92 0 4 0 * b_val_cache[1]
```

### Listing 6.10 q4> fields struct bnode

For a 29th order b-tree each **bnode** contains 30 keys and 31 values. The value array contains either pointers to actual **chunk** structures or pointers to the next lower level of the **b-tree structure**

```
0 0 4 0 int b_key[0]
4 0 4 0 int b_key[1]
-------------------------
112 0 4 0 int b_key[28]
116 0 4 0 int b_key[29]
number of valid key/values in this bnode
120 0 4 0 int b_nelem
124 0 4 0 * b_down[0]
128 0 4 0 * b_down[1]
-------------------------
240 0 4 0 * b_down[29]
244 0 4 0 * b_down[30]
pads to align the structure
248 0 4 0 int pad[0]
252 0 4 0 int pad[1]
```

Now that we have defined the various parts of the b-tree, we need to assemble them.

## Page Lists

The `chunk`, `bnode`, and `broot` structures are of a common size: 256 bytes on narrow systems or 512 bytes for wide systems. As a `region` is initialized, the total number of pages it will map (or at least the number it will start with) is used to calculate the depth of its b-tree. Once this is known, space for the `chunks`, `bnodes`, and the `broot` will need to be allocated. As we noted, all three structures are sized the same. This allows room for a *29th-order* `bnode`. Each `chunk` will hold either 32 or 64 `fld|fld` `dbd` structure pairs, depending on the architecture.

These uniformly sized structures may be conveniently packed into whole memory pages. Once the total space requirements are determined, the kernel allocates enough pages to hold them (see Figure 6-11). This group of allocated page frames is referred to as a page *list*. In most instances not all the space in the page *list* is filled with chunks or bnodes; if the tree grows, these unused fragments are utilized. If we run out of page fragments, the system simply allocates another page and adds it to the `region`'s page *list*.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_203_0.png)

An interesting feature of this model is that pages for the b-trees are allocated from the system's free memory pools the same as pages allocated to a user process. These page allocations do not impact the kernel's memory arenas, and as some b-trees must be very large, this is a good thing. Another feature is that if a process is de-activated, its page *list* may be moved to swap. As process deactivation occurs only in cases of extreme memory pressure, being able to reclaim these extra pages helps vhand perform its task.

If a process has been deactivated and its b-tree has been paged out, we must be able to find these pages and restore them to memory when the process is reactivated. As these pages are not defined by a disk block descriptor entry, the back-store location needs to be stored in the region structure. Since the region structure has a static size, and the number of pages in the page list may vary according to the overall region page count, an interesting method was implemented to find the swapped page list pages. The region r_dbd contains a disk block descriptor to locate the first page of the page list in swap; the disk block descriptor of the second page is stored at the end of the first page, and so on.

This presents a bit of an anomaly. It is said that HP-UX kernel pages are never swapped out, that the kernel is always in-core. Now we see that a region's b-tree may be paged out if its process is deactivated. As a page list is allocated to hold a region b-tree and the region is a kernel structure these pages are kernel pages. So, is the HP-UX kernel ever paged out? The answer is still no, but with the following clarification. Pages initially assigned to the kernel at boot time are considered static kernel pages; those allocated by the kernel later are considered dynamic kernel pages. The kernel never swaps its static pages, but under certain circumstances, such as deactivation, some dynamic pages may be paged out.

Another benefit of this design is that when a process terminates its page list, pages are returned to the system memory pools.

## Connecting the Kernel View to the Process View

We are finally ready to tie the process logical view to the kernel virtual view. To review what we have seen so far, as a process is initialized, the system creates a linked list of region structures in accordance with header information stored in the program file. This information was created and placed in the executable file header by the linking-loader that built the program file. As Figure 6-12 shows, each program's logical regions are linked to an underlying kernel region structure.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_205_0.png)

It is at this level of addressing abstraction that the first level of memory sharing may occur. If two instances of the same program are given process status on the system, they may both share pointers to the same text region. In addition, shared library objects may be mapped by many simultaneous processes. Another level of sharing may occur at the physical level: this is called virtual address aliasing. To understand this feature, we turn our attention to the physical page management features of the HP-UX kernel.

## Managing Page Frames: Many Points of View

As we see in Figure 6-13, there are many ways to view a page frame. It all depends upon whether you are approaching memory from the kernel or a process point of view. So far in this chapter, we have concentrated on the logical and virtual aspects of memory management. Now we get down to the nitty-gritty of managing physical memory.

## Keeping Track of Free Physical Page Frames

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_206_0.png)

Figure 6-13 Managing Page Frames

Our first challenge is simply to know how many physical pages there are, which pages are free, and which have been allocated for use either by a user process or the kernel. To serve this need, HP-UX uses a modified version of an age-old structure called the page free data table, or *pfdt*. The *pfdt* structure has been around in concept since very early UNIX versions, even as far back as Bell Lab System (BLS) releases.

This table is part of the kernel's hardware-independent layer and is not directly connected to the virtual memory translation system. The kernel must manage physical pages and map them to the virtual memory space in alignment with the requirements of the kernel and its processes.

The original incarnation of *pfdt* was quite simple. Each page had a *pfdt* structure, and the entries were arranged in a simple array. The physical page frame number served as the index into the array. As we mentioned in our discussion of the `pfn_to_virt_ptr` structure, modern HP-UX systems must be able to handle partitioned memory configurations. With the advent of today's cell-based systems with their physical and virtual partitioning schemes, this requirement is coming under a new focus. Figure 6-14 illustrates the current incarnation of the page free data table.
