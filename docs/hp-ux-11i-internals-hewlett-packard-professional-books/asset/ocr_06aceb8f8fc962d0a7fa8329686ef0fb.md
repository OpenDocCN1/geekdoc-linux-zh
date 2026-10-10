![](bbox=[0.15, 0.1, 0.85, 0.47])

It is at this level of addressing abstraction that the first level of memory sharing may occur. If two instances of the same program are given process status on the system, they may both share pointers to the same text region. In addition, shared library objects may be mapped by many simultaneous processes. Another level of sharing may occur at the physical level: this is called virtual address aliasing. To understand this feature, we turn our attention to the physical page management features of the HP-UX kernel.

# Managing Page Frames: Many Points of View

As we see in Figure 6-13, there are many ways to view a page frame. It all depends upon whether you are approaching memory from the kernel or a process point of view. So far in this chapter, we have concentrated on the logical and virtual aspects of memory management. Now we get down to the nitty-gritty of managing physical memory.