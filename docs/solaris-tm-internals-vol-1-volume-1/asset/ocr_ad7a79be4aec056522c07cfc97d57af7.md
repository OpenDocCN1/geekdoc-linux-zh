In Solaris, a system class array is initialized at boot time, where each entry in the array is an sclass structure, one for each of the loaded scheduling classes. The sclass structure, shown in Figure 9.3 on page 362, contains the following structure members:

+   - **cl_name** — Pointer to the class name (e.g., TS for timeshare).
+   - **cl_init** — Pointer to the class-specific initialization function (e.g., `ts_init()` for initialization of the timesharing class).
+   - **cl_funcs** — Pointer to a class functions structure; a kernel structure containing pointers to the class-specific functions (e.g., fork, stop, sleep, preempt, etc.).
+   - **cl_lock** — A kernel lock for synchronized access to the class structure.
+   - **cl_count** — A counter maintaining a count of the number of threads attempting to load the class.
+   - **cl_size** — The size in bytes of the class data maintained on a per-thread basis. The size of the structure referenced through the kernel threads `t_cldata` pointer.

The class init routine is called at boot time for all the preloaded scheduling classes. By default, the timeshare and system classes are loaded. The interactive class is dynamically loaded when an X server and Window Manager are started. Only the realtime class is not loaded in a default environment. When a thread is set to the realtime class, with the `priocntl(1)` command or `priocntl(2)` system call, the realtime class module is dynamically loaded by the operating system. You can examine which scheduling classes are currently loaded on the running system with the `dispadmin(1M)` command, as shown below.

```
```text
# dispadmin -l
CONFIGURED CLASSES
===================

SYS        (System Class)
TS         (Time Sharing)
IA         (Interactive)
```
```

Or, for a bit more information, there’s a class function in the crash(1M) utility.

```
```text
# /etc/crash
dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> class
SLOT    CLASS   INIT FUNCTION   CLASS FUNCTION
0       SYS     100fd1d0        1042c5a0
1       TS      10137c2c        1045ef90
2       IA      10137d0c        1045f080
```
```