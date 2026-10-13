
installed on the system, where maxusers equals the number of megabytes of RAM, to a maximum value of 1024 (which equates to 1 gigabyte of RAM—on systems with greater than 1 gigabyte of physical memory, maxusers will be 1024). If maxusers is set in /etc/system, that value is used, up to a maximum value of 2048; any /etc/system maxusers value larger than 2048 results in maxusers getting set to 2048. Once maxusers is established, the startup code sets other kernel limits, based on maxusers in the kernel param_calc() function.

- **maxpid** — Maximum process ID value. If maxpid is set in /etc/system, the maxpid value will be tested against a minimum reserved_procs value (5 in Solaris 2.5.1, 2.6, and 7) and a maximum value (30,000 in all three releases). If maxpid is less than reserved_procs or greater than 30,000, it is set to 30,000. Otherwise, the user-defined value is set.
- **max_nprocs** — Maximum number of processes, systemwide, set as (10 + 16 * maxusers).
- **maxuprc** — Maximum processes per non-root user, set as (max_nprocs - reserved_procs). reserved_procs has a default value of 5.
- **ufs_ninode and ncsize** — High limits for the UFS inode cache and directory name cache. (See “The Directory Name Lookup Cache (DNLC)” on page 568.) Both of these caches are set to the same value, (4 * (max_nprocs + maxusers) + 320).
- **ndquot** — The number of UFS disk quota structures, systemwide, set as ((maxusers * 40) / 4) + max_nprocs.

As you can see, maxusers is not really the maximum number of users the system will support. It’s simply a parameter that can be set to drive the number of several configurable kernel resources that indirectly affect the load or volume of users the system can handle. Many things factor in to the user load capabilities of the system, not the least of which are what constitutes a user, what a user does, and how a user connects to the system.

Other kernel parameters that are related to the STREAMS subsystem and miscellaneous areas of the system are also set at this time. These parameters use hard-coded default values that are not driven by the maxusers parameter unless a value has been set in /etc/system.

- **nstrpush** — Number of STREAMS modules that can be contained (pushed) on a single STREAM; set to 9.
- **strmsgsz** — Maximum size of a STREAMS message; set to 64 Kbytes.
- **strctlsz** — Maximum size of a STREAMS control message.
- **ngroups_max** — Maximum number of groups a user can belong to; set to 16.
- **rstchown** — A boolean that forces POSIX chown(1) behavior, where a process must have an effective UID of 0 (root) to change file ownership; set to 1 (true) by default.
- **hz, hires_hz, hires_tick** — Clock frequency controls. hz is set to 100, hires_hz to 1000, and hires_tick to 0. hz and hires_hz should not be altered. You can set hires_tick to 1 in `/etc/system`. Doing so results in an hz value of 1000, causing the system clock to generate a clock interrupt 1000 times a second (every millisecond) versus the default of 100 times a second (every 10 milliseconds).
- **autoup** — Age in seconds of a dirty page before fsflush will write it to disk; set to 30.
- **rlimits** — Per-process resource limits. Default values are set. Per-process file descriptor limits can be set through `/etc/system`, with `rlim_fd_max` for the maximum value and `rlim_fd_cur` for the current value (current can never exceed the maximum).

For a complete listing of kernel tunable parameters, see [5]. See also Appendix A, “Kernel Tunables, Switches, and Limits”.

Moving along with the system initialization process: The system device name space is established in the /devices directory, based on the device tree created by the OBP firmware. The system call table is initialized, and the kernel loads the device driver classes file, /etc/driver_classes. System parameters are set in the var data structure; most of these parameters are values that we have previously discussed (e.g., max_nprocs), and others are not used in the Solaris kernel (var is a somewhat outdated SVR4 holdover). You can examine the relevant data stored in the var structure with the sysdef(1M) command or with the var function in crash(1M).

Kernel module loading occurs at various points in the boot process. During the platform-specific startup, several core modules, such as the swap, specfs, procfs and tod (time-of-day clock driver), are loaded. Other module loading occurs when a specific kernel subsystem is initialized. For example, the scheduling classes are loaded during the dispinit() function, which initializes the kernel dispatcher subsystem. These modules (and dispinit()) occur before the platform-specific startup returns to the kernel main() function. Other loadable modules that are platform specific are loaded a little later in the process. Examples here include modules specific to the UltraEnterprise E3500 (E6500 servers that support environmental monitoring and specific control functions).

Additional virtual memory support is initialized (the HAT layer and segment drivers), the specfs and swapfs file system support modules are loaded and initialized, the root, swap and dump devices are configured, any kernel modules set for forceload in the /etc/system file are loaded, and the kernel trap table is set (traps were handled through the trap table set in the OBP up to this point). The system displays the memory values for actual, installed physical memory and available memory, that is, what’s left after the kernel consumes whatever pages it requires.

```
mem = 262144K (0x10000000)
avail mem = 257785856
```

Some additional housekeeping, such as creating the interrupt threads and idle thread, is done for the boot processor, clock interrupts are enabled, and the device configuration process is completed. The code walks through the device tree, reading data from the `dev_info` structures created for each device and displaying the device information on the console. Several kernel initialization functions for specific subsystems, such as the callout table, buffer I/O subsystem, credentials and file cache, pseudoterminal and STREAMS support, etc., are invoked through an init table array. Several kernel daemon threads are created, the `init`, `pageout`, and `fsflush` processes are created, and any additional processors (MP system) are initialized.

The process creation of `init`, `pageout`, and `fsflush` is done by means of an internal `newproc()` kernel function, which gets the process table slot and process ID and does some initialization of the proc structure members. An LWP and kernel thread are also created from the `newproc()` function. The `pageout` and `fsflush` processes are actually part of the kernel and execute as kernel threads within the kernel’s address space. The process table entries for these processes are simply placeholders, providing a user-visible view of process execution time (the TIME column from the `ps(1)` command).

The `init` process, also created with a call to `newproc()` from the kernel `main()` function, is the first real user process Solaris creates. Additional work is done by the code path entered when the initial process creation phase (`newproc()`) is completed. First and foremost, a user address space is allocated for the `init` process; it does not attach to or execute in the kernel’s address space. Second, an on-disk binary file—`/sbin/init`—is exec’d once the process initialization is completed. The `pageout` and `fsflush` processes do not have a distinct user address space; instead, they attach to the kernel’s address space. Neither is an explicit `exec()` function called to overlay the newly created process with a new binary image. `pageout` and `fsflush` exist as kernel functions.

Thus, `init` is the first genuine user process created by the system and the last process the kernel must effectively craft piece-by-piece. All further process creation to get to a running system is done by forking `init`, and exec’ing the appropriate binary image from disk.

### 4.2.6 Completing the Boot Process

The remaining phases of the boot process take place under control of the `init` process, which references the `/etc/inittab` file to determine the default init level (typically, 3) and controls the serial execution of several shell scripts in the `/sbin`
