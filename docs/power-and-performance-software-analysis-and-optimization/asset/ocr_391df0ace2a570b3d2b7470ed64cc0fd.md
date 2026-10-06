For example, running this function on a Second Generation Intel® Core™
processor produces:

+   1 ./get-cache
2 (Index 0) 32KB L1 Data Cache [Line Size: 64B]
3 (Index 1) 32KB L1 Instruction Cache [Line Size: 64B]
4 (Index 2) 256KB L2 Unified Cache [Line Size: 64B]
5 (Index 3) 6MB L3 Unified Cache [Line Size: 64B]

# Sysfs

The CPUID leaves described in the previous section can also be accessed via
sysfs interface. In this case, the CPUID leaves are iterated, with the results
cached, when sysfs is initialized. Performing a read(2) on these files
alplus the relevant data in the cache. The code that iterates the information,
alwith the code that executes when these files are accessed can be seen at
$LINUX_SRC/arch/x86/kernel/cpu/intel_cacheinfo.c.

The cache information is stored per logical processor, so the cache sysfs
directory can be found under the sysfs directories, located at /sys/devices/system-
cpu/

For example, looking at the cache cpu0 on the same processor as the
CPUID example from the previous section:

+   1 $ /sys/devices/system/cpu0/cache/
2 index0 index1 index2 index3
3 $ cat /sys/devices/system/cpu0/cache/index0/type
4 Data
5 $ /sys/devices/system/cpu0/cache/index0/size
6 32K
7 $ cat /sys/devices/system/cpu0/cache/index0/coherency_line_size
8 64

# 14.3 PREFETCH

Earlier in this chapter, the principle of data locality was introduced as one of the prime
motivations for utilizing caching. Whereas motivation revolved around temporal
data locality, another observation of data locality can also benefit performance.
The principle of spatial data locality observes that if one address is accessed, other
addresses located near that address are also likely to be accessed.

In order to benefit from this observation, Intel processors support the prefetching
of cache lines. When a cache is prefetched, it is loaded from memory and
placed into one, or levels of the processor cache, not because the executing
code immediately needs it, but because it may need it. If successful, when the cache
is requested, it is already close to the processor, thus completely masking the
memory latency for the load operation. Additionally, since the prefetch occurs