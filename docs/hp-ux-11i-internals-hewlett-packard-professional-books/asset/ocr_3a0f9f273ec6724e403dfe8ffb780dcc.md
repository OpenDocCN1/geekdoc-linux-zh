![](bbox=[0.1, 0.1, 0.9, 0.45])

# Figure 4-1 Static versus Dynamic proc Tables

Prior to the release of HP-UX 11.1, the proc table was a static table, and its size was defined by the system-tunable parameter nproc. The table was an array of data structures of type proc whose starting point was accessed through the kernel pointer proc*. When the table was full, no additional programs could be launched on the system. Increasing the number of allowable processes required a rebuild of the kernel. The current trend is to make many kernel structures dynamic in order to reduce the need to rebuild the kernel (and the number of reboots).

Starting with HP-UX 11.1, the proc table became a dynamic linked list (see Figure 4-1). This arrangement allows for proc table entries to be created on demand and dynamically linked into the list of active processes on the system. Access to the first proc table entry is now made by following the kernel pointer proc_list*. Each table structure is still defined as a proc (note that this structure definition has changed significantly since previous releases), which now contains the linkage pointer p_next* to the next proc table entry.

The kernel-tunable parameter nproc is still used, but its purpose has changed somewhat: it is now used to define a maximum number of allowable proc table entries that may be created on the system. The kernel can maintain many static lists, which need to be sized large enough to handle the kernel’s worst-case needs. The nproc parameter has been used to help in this task during kernel initialization. Until these tables also become dynamic structures, a parameter like nproc will be required.

The process has long been the workhorse of the HP-UX runtime environment. With the release of HP-UX 10.0 came the introduction of the thread as the schedulable entity.