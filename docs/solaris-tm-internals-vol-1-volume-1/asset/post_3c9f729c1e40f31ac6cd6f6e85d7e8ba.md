
Now, let’s put a process in the realtime scheduling class; process PID 833 is a test program which just sleeps for a minute, then exits.

```text
# priocntl -s -c RT -i pid 833
```

Then, we’ll take another look at which scheduling classes are loaded on the system:

```text
# dispadmin -l
CONFIGURED CLASSES
==================

SYS       (System Class)
TS        (Time Sharing)
IA        (Interactive)
RT        (Real Time)

# /etc/crash
dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> class
```

| SLOT | CLASS | INIT FUNCTION | CLASS FUNCTION |
| --- | --- | --- | --- |
| 0 | SYS | 100fd10 | 1042c5a0 |
| 1 | TS | 10137c2c | 1045ef90 |
| 2 | IA | 10137d0c | 1045f080 |
| 3 | RT | 102045b8 | 7802f6e8 |

The class function in crash(1M) provides the class name, the kernel virtual address of the init function for that class, and the address of the class operations table, also known as the class functions structure or class operations vector table. (Operations vector table is a generic term that describes an array of pointers to functions, which is precisely what the class functions (`cl_funcs`) structure is.)

The class functions structure bundles together function pointers for all of the class-specific (scheduling-class-dependent) kernel routines. They essentially fall into one of two categories: class management and thread control. The kernel switches in to the appropriate routine for a specific scheduling class, using essentially the same method used in the vfs/vnode subsection. A set of macros is defined; the macros resolve to the class-specific function by indexing through either the current kernel thread pointer or the system class array. Both the system class array and kthread structure maintain a pointer to the class functions structure. For example, the class-specific enterclass and exitclass functions are indexed through the system class array. (The functions must be called to enable a thread to enter or exit the scheduling class because the kernel thread link to the class operations table would not yet be in place.) The macro for the enterclass function is shown below.

```c
#define CL_ENTERCLASS(t, cid, clparmscp, credp, bufp) \
        (sclass[cid].cl_funcs->thread_cl_enterclass) (t, cid, \
                (void *)clparmscp, credp, bufp)
```

### Header File <sys/class.h>

The argument list for the `enterclass` routine follows the macro name `CL_ENTERCLASS`. On the second line, the system class array, `sclass[]`, is indexed, using the class ID (`id`: each loaded scheduling class has a unique class ID). From there, the pointer to the class functions table, `cl_funcs`, gets us to the class-specific `cl_enterclass` code. An example of a macro that uses the kernel thread `clfuncs` pointer is the preempt routine.

```c
#define CL_PREEMPT(tp) (* (tp)->t_clfuncs->cl_preempt)(tp)
```

### Header File <sys/class.h>

Here, `tp` is a pointer to the current kernel thread, and the `cl_preempt` code is entered through the thread’s `t_clfuncs` pointer to the class functions table.

Below is a complete list of the kernel scheduling-class-specific routines and a description of what they do. More details on many of the functions described below follow in the subsequent discussions on thread priorities and the dispatcher algorithms. Each routine name is listed to indicate which scheduling class provides code for a given function. The first five functions fall into the class management category and, in general, support the `priocntl(2)` system call, which is invoked from the `priocntl(1)` and `dispadmin(1M)` commands. `priocntl(2)` can, of course, be called from an application program as well.

-   **ts_admin, rt_admin** — Retrieve or alter values in the dispatch table for the class.
-   **ts_getclinfo, ia_getclinfo, rt_getclinfo** — Get information about the scheduling class. Currently, only the max user priority (`xx_maxupri`) value is returned.
-   **ts_parmsin, ia_parmsin, rt_parmsin** — Validate user-supplied priority values to ensure they fall within range. Also check permissions of caller to ensure the requested operation is allowed. For the TS and IA classes, a limit check is done against the max user priority (`maxupri`). For the RT class, the notion of a user priority does not exist, so a range check is made against the max RT priority. The functions support the `PC_SETPARMS` command in `priocntl(2)`.
-   **ts_parmsout, rt_parmsout** — Support `PC_GETPARMS` command in `priocntl(2)`. Retrieve the class-specific scheduling parameters of a thread.
-   **ts_getclpri, rt_getclpri, sys_getclpri** — Get class priority ranges. For each scheduling class, return the minimum (lowest) and maximum (highest) global priority.

The following functions are for thread support and management.

-   **ts_enterclass, rt_enterclass, sys_enterclass** — Allocate the resources needed for a thread to enter a scheduling class. For the TS class, a `tsproc` structure is allocated. If the requested class ID is IA (remember, IA class threads use a `tsproc` structure and most of the TS support code), make sure the caller is either root or a member of the windowing system process group. Initialize the `tsproc` structure members with either user-supplied values (after validating values and permissions) or default values, and add it to the linked list of `tsproc` structures. Follow the same procedures as for RT class. The SYS class routine is just a stub that returns 0; since there is no system-class-specific data structure, there’s nothing to allocate or initialize.
-   **`ts_exitclass`, `rt_exitclass`** — Remove the class-specific data structure (`tsproc` or `rtproc`) from the linked list and free it.
-   **`ts_fork`, `rt_fork`, `sys_fork`** — Process fork support code. Allocate a class-specific data structure (`tsproc` or `rtproc`), initialize it with values from the parent thread, and add it to the linked list. The SYS fork is a no-op. It is called from the `lwprocess()` and `lwpfork()` kernel functions as part of the fork(2) system call kernel code when a new process is created.
-   **`ts_forkret`, `rt_forkret`, `sys_forkret`** — Called from the kernel `cfork()` (common fork) code in support of a fork(2) system call. It is the last thing done before the fork(2) returns to the calling parent and the newly created child process. The `xx_forkret` functions resolve the run order of the parent and child, since it is desired that the child run first so the new object can be exec’ed and can set up its own address space mappings to prevent the kernel from needlessly having to duplicate copy-on-write pages. In the TS class, the child is placed at the back of the dispatch queue and the parent gives up the processor. This is handled in another class routine, `ts_run`.
-   **`ts_parmget`, `ia_parmget`, `rt_parmget`** — Get the current priority and max user priority for a thread. The functions are called from the `priocntl(2)` system call. `ts_upri` and `ts_uprilim` from the class-specific structure (`tsproc`, `iaproc`) are returned. IA class threads also return the `ia_nice` field. For RT threads, the `rt_pri` and `rt_pquantum` from the `rtproc` structure are returned.
-   **`ts_parmset`, `ia_parmset`, `rt_parmset`** — Set the priority of a thread on the basis of passed input arguments. A user parameter data structure is defined for each scheduling class: `iaparms`, `tsparms`, and `rtparms`. For the IA and TS class, a user priority limit and user priority value can be set. The support code checks the user priority or priority limit when a `priocntl(2)` is executed to ensure the values fall within the boundary values for the class and also checks credentials to ensure the caller has permission to alter the thread’s priority. Valid user-supplied priorities for TS/IA class threads are set in the `ts_upri` field in the `tsproc` structure and factor in to priority adjustments on the thread.

RT class threads do not support the notion of user-supplied priorities in the same manner as do TS/IA class threads. Where user-supplied priorities for TS/IA threads nudge the actual thread priority in one direction or another, a user-supplied priority for RT class threads directly maps to the RT thread’s global priority. Details are provided in “Thread Priorities” on page 375.
