# Solaris Memory Architecture

![](bbox=[0.135, 0.09, 0.915, 0.532])

The segment driver
fault handler is called
to handle the fault by
bringing it in from
swap.

Vnode Segment Driver
segvn

```
seg_fault()
```

```
segvn_fault()
```

vop_get_page()

sun4u
hat layer
sun4u-
sf-mmu

Page Fault
(trap)

```
swapfs
```

A byte is touched in
the heap space, causing
an MMU page fault.

Swap
the page is
copied from
swap to memory.

Page

# Figure 5.8 Virtual Address Space Page Fault Example

In the figure, we see what happens when a process accesses a memory location
within its heap space that does not have physical memory mapped to it. This
most likely occurred because the page fault of physical memory has previously been-
len by the page scanner as a result of a memory shortage. In the numbered events
in we see:

+   1. A reference is made to a memory address that does not map to a physical
page of memory. In this example, the page has been paged out and now
resides on the swap device.

+   2. When the process accesses the address with no physical memory behind it,
the MMU detects the invalid reference and causes a trap to occur on the pro-
cessor executing the code of the running thread. The fault handler recognizes
this as a memory page fault and establishes which segment the fault occurred
in by comparing the address of the fault to the addresses mapped by each
segment.

+   3. The address space as_fault() routine compares the address of the fault
with the addresses mapped by each segment and then calls the page_fault
routine of the segment driver for this segment (in this case, the vnode seg-
ment driver).