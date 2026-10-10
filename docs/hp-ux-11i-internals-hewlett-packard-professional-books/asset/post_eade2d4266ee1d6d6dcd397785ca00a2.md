
As soon as we get above the **desfree** limit, we consider deactivated processes for reactivation. Even if we reactivate a large process, we may be able to stay above the limit, since pages are only reloaded on an on-demand basis.

## Reservation Versus Swap Allocation

In operating system design, there are many variations of swap management. Some systems dynamically assign swap space from available file system space and return it when it’s not needed. Others configure static, dedicated swap at boot time and force the system to work within its boundaries. Some allow swap space to be allocated on the fly from either dedicated volumes or by creating a directory under a mounted file system and creating swap files there.

An important design consideration is how the system responds if it runs out of swap space. Will the kernel crash or simply terminate the process that made the swap request? This could have severe impact on running applications and wreak havoc on system uptime.

A final issue is when to allocate a swap page for a process page. Some systems make an entire copy of a program to swap prior to running the first command. These allocated swap pages belong to the process as long as it is active and are reclaimed by the swap system only at process termination. Another approach is to hand out swap locations as they are needed and return them to a free list as soon as their pages are reloaded into memory. In this model, a page may be swapped several times during its life cycle, and it might use a different swap location each time. This approach means we have to go through the overhead of allocation each time the page is to be swapped. We could also wait to assign a page until it is needed and then keep the allocation until the process terminates. In this last model, we would have to pay the price of allocation only once. Each approach has its pros and cons.

HP-UX uses bits and pieces of the two approaches and adds a few twists of its own. The HP-UX paging strategy keeps track of the number of reserved, allocated, and free swap pages under its control.

When a process requests permission to become active via the **fork()** or **vfork()** system calls, the system calculates the total number of swap pages this process might need. It uses a worst-case calculation and includes room for all of the process’s data pages, **region** page lists, **aarea**, and any other process-specific writable memory pages. This number of pages is then subtracted from the system’s swap reservation limit. In this way, HP-UX performs prereservation and postallocation of swap.

To understand this approach, think of a fancy restaurant. You plan to bring a party of 12 to the restaurant for dinner on Friday night at 7:00 p.m. If you wait until Friday and simply show up with your group, you may have to wait a long time for seating. Although you may eventually get to eat, your enjoyment of the experience may be adversely affected by the long wait. To avoid customer dissatisfaction, the restaurant takes seating reservations ahead of time. You call the restaurant on Tuesday to make a reservation for you and your party on Friday. When you call the maitre d’ and request seating for Friday, he or she checks a list and lets you know if the restaurant can accommodate you at that specific time. If it can, the maitre d’ takes your name and confirms the reservation.

Now let’s think about this process a bit. Does the maitre d’ know exactly where you will be seated? Does he or she know what you will order or how long you plan to stay? The only thing the maitre d’ can assume is that the restaurant’s resources—tables and chairs, capacity of wait staff and kitchen—will need to accommodate your party. The establishment determines a reservation limit dependent upon its capacity. When you actually arrive at the restaurant, the decision is made to allocate specific resources to you as they are required. Once you are seated, the space remains yours until your evening is finished. If you get up to have a spin on the dance floor or go to the powder room, the resources assigned to you and your party are maintained. When you pay your check and leave, the resources are collected and made available for the next party. If you hadn’t shown up on Friday, or if your party ended up being only 8 instead of 12, no resources were wasted; they simply remained available to accommodate other customers as required.

This is a fairly decent analogy of the HP-UX swap reservation policy. Once a page has been allocated to hold a specific page, it is retained for this purpose until the process exits, then it is returned to the swap map as a free page. In Figure 7-4, we see the relationship between swap space, reservation, and allocation.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_229_0.png)

At boot time, the reservation limit is set to the total amount of configured swap space. When the system is asked to `fork()` a new process, its potential swap requirements are subtracted from the swap reservation. If this causes the limit to go negative, the `fork()` fails and the error message returned will indicate the failure was due to insufficient swap.

If the `fork()` succeeds, the reservation limit is adjusted and the process is initialized. At this point, no pages have actually been allocated, only reserved. On a system with ample physical memory, it is quite possible that the process will never have a swap page allocated. This is the ideal, as it means system memory pressure never triggered the paging system.

When a page needs to be swapped for the first time, the kernel allocates a page from the swap map and pages the in-core page to the newly allocated swap page. When this occurs, the allocated count is incremented and the reserved count is decremented; the reservation limit remains unchanged. The swap reservation limit plus the number of reserved and allocated pages should always add up to the total amount of swap configured on the system. Once a page allocation has been made, it is maintained until the process is terminated.

## A Simple Swap Example

Figure 7-5 demonstrates a simple swap scenario: three programs would like to run in our model. The model is configured with 12 pages of physical memory and 12 pages of swap space.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_230_0.png)

The swap reservation limit is 12 when progA asks to run. Its swap requirement is four pages for data; 12 - 4 = 8, so the reservation limit is adjusted and the process is given the green light.

When progB asks to run, its swap requirement is determined to be five pages. The reservation limit is checked: 8 - 5 = 3, so this process is also given the green light.

When progC asks to join the club, it is denied permission to run. Its swap requirement is four pages. Since 3 - 4 = -1, this would result in a negative swap reservation limit, so the `fork()` fails.

You might ask why we don't just let all three run. The total memory requirement appears to be 21 pages, and we have a total of 24 pages counting physical memory and swap. If we returned freed pages to the swap map as they are paged back into core, we could get by. The approach HP-UX takes is on the conservative side but assures reasonable performance. Stopping to allocate a swap page is a timely operation, and we don't want to do this more than once for a page. If your kernel is scheduling page-outs, HP-UX chooses a strategy that allows us to minimize the overhead of the paging system at a time when performance is already being compromised by high memory pressure.

Another issue is that we don't want to find ourselves in the situation where a page needs to be swapped and the system is simply out of swap. When this happens, a kernel either has to panic or at the very least kill the process that is causing the memory pressure. The HP-UX approach is to never allow this scenario by simply assuring that sufficient swap space is configured before allowing a process to start. With the current cost of disk storage, large swap space should not be considered a major issue.

Let's revisit our simple model. Suppose you decided to double the amount of physical memory on the system so that you would never have to swap. This sounds like a good idea and should guarantee optimum performance as far as memory pressure is concerned. The problem arises when we work through the model: if we don't also increase our swap space we won't be allowed to schedule all three processes, since we will still run out of swap reservation space before we can launch progC. In our model it seems simple to adjust the swap space, but in the real world and with the large configurable memory options available today, this isn't always practical.

On early versions of HP-UX, when you wanted to increase the physical memory to eliminate the need for swap, you still had to provide the swap space to satisfy the swap reservation scheme. Customers did not want to buy swap space that might not even be used, and who could blame them? In those days, disk space was a much more valuable commodity. One approach would have been to simply turn off swap preservation, but this would lead to the problems discussed earlier. The answer arrived at by the HP-UX kernel designers is a feature called pseudo-swap.

## Pseudo-Swap

The pseudo-swap approach is one of the least understood features of the HP-UX kernel; hopefully, we can make you comfortable with its purpose and function. Pseudo-swap is enabled in the HP-UX kernel by setting the kernel parameter swappemon to 1 (this is the default for freshly installed systems). With pseudo-swap enabled, the swap reservation limit is adjusted to include all physical swap plus 75 percent of the system's available memory (87 percent on the latest release). This has been described as "using physical memory for swap space." While there is a basic truth to this statement, it doesn't tell the whole story. Although pseudo-swap may
