bottom-half queue bitfield is set (we marked it at point 4). We'll enter timer_bh(), which will update the system time (according to lost_ticks) and run the timers (both old and new timers). All these operations will run from bottom-half context, which from a hardware point of view is still an IRQ context.

When timer_bh returns (after all timers have been executed and rotated), we'll effectively return from the timer interrupt.

The difference between uniprocessing (UP) and symmetric multiprocessing (SMP) is that in UP the point (6) is executed within the timer IRQ. On IA-32 SMP, point (6) is not executed within the timer interrupt handler; the timer IRQ skips it completely. We instead broadcast a special SMP timer IRQ to all CPUs and we run only point (6) within the ioapic local timer IRQ.

# ## System Initialization and Boot

Most Linux distributions boot by means of the initrd facility, which adds the capability to load a RAM disk by the boot loader. This RAM disk can then be mounted as the root file system and programs can be run from it. Afterwards, a new root file system can be mounted from a different device. The previous root (from initrd) is then either moved to the directory /initrd or it is unmounted. This is how Linux bootstraps the kernel image into memory and then mounts the real file system.

The initrd utility is mainly designed to allow system startup to occur in two phases, the first where the kernel comes up with a minimum set of compiled-in drivers, and the second where additional modules are loaded from initrd.

When using initrd, the system boots as follows:

+   1. The boot loader loads the kernel and the initial RAM disk.
+   2. The kernel converts initrd into a “normal” RAM disk and frees the memory used by initrd.
+   3. initrd is mounted read-write as root.
+   4. The /linuxrc is executed (this can be any valid executable, including shell scripts; it is run with uid 0 and can do basically everything init can do).
+   5. When linuxrc terminates, the “real” root file system is mounted.
+   6. If a directory /initrd exists, the initrd is moved there. Otherwise, initrd is unmounted.