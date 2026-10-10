priority of 1, and if the priority is not specified to the `swapon` command, it assumes a default priority value of 1 as well. Device swap takes precedence over file system swap at the same priority, but file system swap at a stronger priority takes precedence over device swap at a weaker priority.

When two or more device or file system swap areas share the same priority, space is allocate from them in a round-robin fashion. This round-robin scheme is employed at the swap chunk level, not at the individual page level.

# # Tracking Swap in the Kernel Structures

In Figure 7-7, we see the relationship between the various kernel-resident data structures required to manage the swap space.

![](bbox=[0.2, 0.36, 0.8, 0.73])

As we see in the diagram, the hambone is connected to the knee bone. Swap management starts with entries in the swap device table, `swdevt`, and the file system device table, `fswdevt`. Pointers from the two priority arrays are used to order the searching of the swap devices. A swap device is broken down into individual swap chunks. The kernel tunable `maxswapchunks` sets the systemwide number and determines the *size* of the swap table. Each swap chunk is sized by the kernel-tunable `swchunk`, which defaults to 2 MB, enough room for 512 page-outs.