# CHAPTER 5 Designing Experiments

tmpfs, a mount point must be created, the files must be copied to that location, which effectively loads the files into memory, and then the application can interact with the files stored at mount point.

Many Linux distributions maintain a tmpfs mount at /dev/shm/. Some distributions also use tmpfs for /tmp/. This can be easily verified by running:

```
$ grep tmpfs
```

Adding a tmpfs mount point is as simple as running:

```
# mkdir tmp_dir
$ mount -t tmpfs tmpfs tmp_dir
```

The second technique, using the mmap(2) system call, allows an application to map files or anonymous pages into the process's address space. This then returns a pointer to the beginning of the file's memory address, allowing for the application to manipulate it, like would incur any data in memory. Paging in Linux is performed lazily, that is, the page mappings are added to the process but the data is not retrieved from disk until the first page fault to page. To avoid this page overhead from occurring during the measurements, use the MAP_POPULATE flag for mmap(2), which causes the pages to be loaded immediately.

Serving out resources from memory, as opposed to the network or disk, will greatly decrease the variance present in our experiments. If the resources are small enough to fit into the LLC, it is possible to go even further, by iterating the data to warm the cache. This ensures that memory access actually hits memory during the measurements. Of course, this assumes that the measurement is focusing on the processor pipeline efficiency, for an algorithm that is invoked with cache warm data. Data can be saved with cold cache from memory by ensuring cache line alignment and using the clflush or nontemporal store instructions.

Now that our microbenchmark has accounted for variance in items 1 through 4, it's time to look controllable sources of variance during the actual rendering measurement. Variance can be introduced by CPU power-saving features, such as P and C states, as well as some features designed to improve CPU performance, for example, Intel® Turbo Boost and Intel® Hyper-Threading Technology. Often these can be temporarily disabled in the BIOS. The author does not recommend disabling them for any longer than the test duration.

The variance introduced via P states and Intel Turbo Boost from the instance, of varying clock frequencies between measurement runs. For instance, the clock speed 800 MHz for one run, and 1.6 GHz for another. In the deeper C states, such as C6, the caches are powered down and thus invalidated, previously warm cache to turn cold. If P states cannot be disabled, the Linux kernel's cpufreq scaling driver, CONFIG_CPU_FREQ, can be used in conjunction with the performance governor. This will keep the CPU frequency constant between tests.

Another source of variance is CPU migrations, where the process moves from executing on one processor to another, again leading to situations where the cache