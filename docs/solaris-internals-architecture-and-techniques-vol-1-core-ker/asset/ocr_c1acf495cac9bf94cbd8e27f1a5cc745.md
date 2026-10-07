# The Solaris Multithreaded Process Architecture

fork() or fork() or vfork()
cckproc()
getproc

Get proc structure (via kmem_cache_alloc(process_cache)).
Set process state (p_stat) to SIDL.
Set process start time (p_mstart).
Call pid_assign() to get PID.
pid_assign())
Get a pid structure.
Get a /proc directory slot.
Get an available PID.
init the PID structure.
Set reference count.
Set PID.
Return pid to getproct().

Check for process table overflow (procs > v.v_nprocs).
Check for per-user process limit reached.
Put new process on table linked list.
Set new process p_ignore and p_signal from parent.
Set the following fields in new (child) process from parent.
Session structure pointer p_sess.
Executable void pointer p_exec.
Address space fields p_brksize, p_stksize
Set child PID.
Set parent-child-sibling siblings.
Copy process state from parent to child, p_prof.
Increment reference counts in open file list

(child inherits these)
Copy parent's users to child (includes copying open file list)
if (child inherits /proc tracing flag (SPROK set in p_flag)
Set p_sigmask in child from parent.
Set p_fitmask in child from parent.

else
Clear p_sigmask and p_fitmask in child (set to empty).
if (inherit multicast accounting in parent)
Enable multicast accounting in child
Return from getproc() to cfork().

if (vfork())
Set child address space to parent (child p_as = parent p_as).
Set child VFS in p_flag.
else (not a vfork())
Duplicate copy of parent's address space for child (as_dup)
Duplicate parent's shared memory for child.
Duplicate parent LWP s and kthreads.

if (fork())
Just duplicate the current thread.
forkl())
lwp_create()
else (walk the process thread list - p_list; for each thread)
forkl())
lwp_create() - create an LWP
Replicate scheduling class from parent
thread_count() - create a kernel thread

Add the child to the parent's process group (pgjoin())
Set the child process state (p_stat) to SRUN
if (vfork())
Increment cpu_sysvfork fork count (cpu_sysvfork.sysfork)
Call continuelwp() for child execution before parent

else
Increment cpu_sysvfork fork count (cpu_sysvfork.sysfork)
Place child in front of parent on dispatch queue
(so it runs first)

Return values: PID to parent, 0 to child