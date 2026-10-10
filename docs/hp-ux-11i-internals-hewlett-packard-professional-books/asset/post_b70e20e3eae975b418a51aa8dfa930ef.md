
sound a bit strange at first, it provides several benefits over simply turning swap reservation off. Figure 7-6 illustrates the addition of pseudo-swap to the mix.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_232_0.png)

The addition of pseudo-swap allows the actual swap space to be reduced to as little as 25 percent of the physical memory. That's not to say that you *should* reduce it—just that you *can*. If the system is configured with ample physical memory, then there is no danger in reducing the size of the swap map. If, however, memory pressure increases and we don't have actual swap space to handle it, things can get a bit interesting. Consider the following scenarios:

- **First scenario:** We have enough physical memory for all the system and user needs. Pseudo-swap is turned on, and device swap is reduced to 25 percent of the available memory. No problem—this should work just fine.
- **Second scenario:** You have maximized your physical memory, but your processes simply want more! It's easy: configure the amount of swap your processes need. In this scenario, we recommend that you leave pseudo-swap disabled, as you would really prefer to have device swap fulfill the system's paging requirements.
- **Third scenario:** Originally we had sufficient memory, turned on pseudo-swap, and reduced the physical swap to a minimum. The challenge is that we have since increased our demand on memory by adding more processes, but we haven't upgraded the memory or the swap space. What happens when we start using the pseudo-swap to satisfy our system needs?

When a process starts, its swap space requirements are calculated and reserved. As long as there is device or file system swap space available to cover this reservation, all is fine. Once we exceed the physical swap limit, we begin to allocate from the pseudo-swap area. As swap is reserved for a new region, if it falls within pseudo-swap, then its pages are not reserved; instead, they are allocated right from the start. In either case, this has the same net effect on the reservation limit, but the dynamics of this region with respect to vhand are quite different.

The mechanics of pseudo-swap are that if a swap space cannot be reserved against the available physical swap during the creation of a memory region, then it is flagged as being preallocated in pseudo-swap (this is actually noted in the region's pointing to the region). On the surface, this almost sounds logical! We need to make room in memory, so we move a page to swap, but if the swap page we move it to is in memory (pseudo-swap), we haven't gained anything—we haven't increased the freemem count. This is the case, but the important issue is that swap didn't fail. We just didn't accomplish the desired goal this time, so hopefully, vhand will continue and try to steal a page with an actual reserved or allocated back-store page.

Once we start allocating from pseudo-swap, in effect, the number of pages available for paging in is reduced. If a page is mapped by a region that has been marked as a pseudo-swap region, then all attempts to swap one of its pages simply result in the page remaining where it is. Conceptually, the swap would be successful but at a net-sum-gain of zero as far as increasing the value of freemem is concerned. To avoid wasting vhand's time, regions identified as containing pseudo-swap pages are not eligible for inclusion in the vhand algorithms. When agehand or stealhand points to the pregion of a pseudo-swap region, r_swapmem, it simply moves on to the next region in the chain.

As pseudo-swap is allocated, it has the effect of reducing the number of physical pages that may be paged out in times of high memory pressure. A process lucky enough to have its pages in pseudo-swap regions will continue to operate with little impact because its pages are, in effect, locked in memory. But those processes resident in the remaining pages will suffer a performance hit because their pages must carry the extra burden of being at risk of being aged and stolen by the paging system.

## Interpreting the Output of swapinfo

If you run the swapinfo command and have pseudo-swap enabled, you will see a line that reports the amount of memory swap available and the amount currently in use. Don't be surprised if pseudo-swap usage is reported even when no physical swap has been allocated. Since pseudo-swap is letting us cheat the limit, the system must be able to adjust this cheat as the kernel takes dynamic pages out of circulation, effectively reducing the available memory count. Therefore, the system reports these kernel-allocated pages as allocated pseudo-swap pages. This effectively reduces the swap reservation limit available and keeps the system from overcommitting its memory resource.

Pseudo-swap works well for its intended purpose, but if you push it past the limits, you will have slower overall system performance—but everything will still run. Don't be afraid of pseudo-swap, but make sure you understand its purpose.

## Device Swap

Device swap is dedicated physical or logical disk volumes. These raw volumes are configured for exclusive use by the swap system. If logical volumes are used, you should attempt to have only one swap space per physical disk controller. It is much better to have one large volume than two smaller ones sharing the same spindle.

It is a common practice to also configure swap devices as dump devices; this may be done either through inclusion in the kernel's "system" file when the kernel is being built or through lines placed in the /etc/fstab file. The use of the /etc/fstab file gives you more control and makes it easier to modify your configuration. If a swap area is added to /etc/fstab it may be activated by issuing the swapon -a command. If a swap area definition is being removed from /etc/fstab a system reboot is required to halt its use. There is no swapoff command for HP-UX.

## File System Swap

As the name suggests, we may also allocate swap space from swap files reserved on mounted file systems. The swap files are sized in alignment with the swap chunk size (the swap chunk is the basic unit used to track swap in kernel data structures, we will discuss it in detail shortly) and may be dynamically allocated as needed. When a file system swap space is initialized, a minimum and maximum amount of space may be configured. A reserved free space limit for the file system may also be specified.

Initialized file system swap appears as a directory named paging, which contains individual swap files. The swap file naming convention is somewhat interesting. The root of the name is the system's hostname followed by a period (.) and the swap chunk number this file represents in the system's swap table. While file system swap spaces are fully functional, they do present a couple of concerns. When a file system is 100 percent full, its performance becomes sluggish, and a file system with a paging directory and swap files may not be unmounted. If the host file system employs features such as VxFS logging, this could further impact swap performance. Keep these issues in mind before deciding to use this feature.

It is entirely possible to allocate file system swap on a remotely mounted Network File System (NFS), but this is generally not a good idea. The extra overhead incurred in the network combined with the stateless nature of an NFS mount makes for very bad chemistry! Besides, the NFS server's administrator may not appreciate your chewing up their disk space to satisfy your swap requirements (such connections are readily apparent, and with the naming convention used, it is a simple matter to determine which remote host has configured the remote swap).

## Swap Priority

Both types of swap, device and file system, may be assigned a priority in the range of 0 to 10. Priority 0 devices are used first, and 10 are used last. The primary boot swap device is assigned a priority of 1, and if the priority is not specified to the `swapon` command, it assumes a default priority value of 1 as well. Device swap takes precedence over file system swap at the same priority, but file system swap at a stronger priority takes precedence over device swap at a weaker priority.

When two or more device or file system swap areas share the same priority, space is allocated from them in a round-robin fashion. This round-robin scheme is employed at the swap chunk level, not at the individual page level.

## Tracking Swap in the Kernel Structures

In Figure 7-7, we see the relationship between the various kernel-resident data structures required to manage the swap space.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_235_0.png)

As we see in the diagram, the hambone is connected to the knee bone. Swap management starts with entries in the swap device table, `swdevt`, and the file system device table, `fswdevt`. Pointers from the two priority arrays are used to order the searching of the swap devices. A swap device is broken down into individual swap chunks. The kernel tunable `maxswapchunks` sets the systemwide number and determines the *size* of the swap table. Each swap chunk is sized by the kernel-tunable `swchunk`, which defaults to 2 MB, enough room for 512 page-outs.
