# (1GB Example)

![](bbox=[0.097, 0.103, 0.853, 0.497])

# Amount of Free Memory

Figure 5.24 Scan Rate Interpolation by the Priority Paging Algorithm

The algorithm pages only against the file system cache when memory is between cachefree and lotsfree by skipping pages that are associated with the swap device (heap, stack, copy-on-write pages) and by skipping file pages that are mapped into an address space with execution permission (binaries, shared libraries).

The new algorithm has no side effects and should always be enabled on Solaris versions up to Solaris 7. (Note: The algorithm has not been replaced in Solaris 8 by a new cache architecture, and priority paging should not be enabled on Solaris 8.) It was not enabled by default in Solaris 7 only because it was introduced very late in the Solaris release cycle.

# 5.8.4.1 Page Scanner CPU Utilization Clamp

A CPU utilization clamp on the scan rate prevents the page-out daemon from using too much processor time. Two internal limits govern the demand and maximum CPU time that the scanner should use. Two parameters, min_percent_cpu and max_percent_cpu, govern the amount of CPU that the scanner can use. Like the scan rate, the actual amount of CPU that can be used at any given time is interpolated by the amount of free memory. When memory is at lotsfree (cachefree with priority paging enabled) to max_percent_cpu if free memory were to fall to zero. The defaults for