sound a bit strange at first, it provides several benefits over simply turning swap reservation off. Figure 7-6 illustrates the addition of pseudo-swap to the mix.

![](bbox=[0.12, 0.18, 0.82, 0.48])

The addition of pseudo swap allows the actual swap space to be reduced to as little as 25 percent of the physical memory. That's not to say that you *should* reduce it—just that you *can*. If the system is configured with ample physical memory, then there is no danger in reducing the size of the swap map. If, however, memory pressure increases and we don't have actual swap space to handle it, things can get a bit interesting. Consider the following scenarios:

+   * **First scenario:** We have enough physical memory for all the system and user needs. Pseudo-swap is turned on, and device swap is reduced to 25 percent of the available memory. No problem—this should work just fine.
+   * **Second scenario:** You have maximized your physical memory, but your processes simply want more! It's easy: configure the amount of swap your processes need. In this scenario, we recommend that you leave pseudo-swap disabled, as you would really prefer to have device swap fulfill the system's paging requirements.
+   * **Third scenario:** Originally we had sufficient memory, turned on pseudo-swap, and reduced the physical swap to a minimum. The challenge is that we have since increased our demand on memory by adding more processes, but we haven't upgraded the memory or the swap space. What happens when we start using the pseudo-swap to satisfy our system needs?

When a process starts, its swap space requirements are calculated and reserved. As long as there is device or file system swap space available to cover this reservation, all is fine. Once we