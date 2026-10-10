It’s possible for the system to perform *compaction*, but such an operation must be carefully evaluated with respect to its cost and benefit. Compaction shifts one or more processes so that all the free space is contiguous. It is an expensive operation because process must be stopped while they are shifted and all the address inside the process must be changed to refer to the new addresses.

If the memory allocation had been prescient, it might have ended up with the allocation shown in Figure 4.13g. This could not happen with the “lowest large-enough space” rule described above. In fact, there is no general rule which always results in the best outcome.

# Memory Overlays

Another extension to non-mapped memory relies on partitioning $^{6}$ a program into components such as

+   - Common
+   - Initialization
+   - Main subroutine
+   - Shutdown

At the start, only the Common component is loaded. When it starts, the Initialization code is loaded into an *overlay* area; when the Initialization is finished, the Main subroutine overlays the Initialization code; when the Main subroutine is finished, the Shutdown code overlays the Main subroutine code $^{7}$. The benefit to overlays can be seen in Figure 4.14 where it is obvious that the whole program cannot fit into memory, but the critical parts can be loaded as they are needed.

> $^{6}$ Some systems perform the partitioning through an automatic mechanism while others require explicit programmer declarations.
> $^{7}$ Some systems make the overlay operation a transparent part of a subroutine call while others require explicit system calls to load an overlay.