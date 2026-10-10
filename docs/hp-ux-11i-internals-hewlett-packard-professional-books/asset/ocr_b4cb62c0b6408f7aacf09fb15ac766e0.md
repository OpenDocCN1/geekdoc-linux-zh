because it was set during the copy process and we need the next access to fault and reload the access rights from the newly created pdlr entry. Now we are ready to continue using our new private copy of the data.

# ## Copy-on-Write for the Parent, Copy-on-Access for the Child

Before we move on, let’s talk a bit about the older copy-on-write/access mechanics. In most cases, it behaves similarly to copy-on-write except that virtual page alias entries are not utilized and all first access by a child results in a private copy being made.

If the kernel parameter `COW`=1, copy-on-write is used for duplication of all `r_type`=`RT_SHARED` regions. Currently, the HP-UX kernel defaults to `COW`=0 and uses copy-on-write/access. The exception is in the case of private text regions encountered in `EXEC_MAGIC` programs, where it always uses copy-on-write (first implemented with the HP-UX 10.0 release). This parameter is not user-tunable in HP-UX 11.x and may only be changed using `adb` (not for the faint of heart).

In HP-UX 10.x, the COW was a user-tunable parameter. Why this has been changed remains a bit of a mystery, since Hewlett-Packard has stated it intends to move completely to copy-on-write in the future.

It’s time to return to our discussion of duplicating a process’s memory view during a `voff()`. A special case exists when the region to be copied holds the current thread’s `uarea`.

# ## Creating the New uarea

The `pregion` referencing the parent’s `uarea` is somewhat of a special case and is replaced by one for a new `uarea` created for the child’s initial thread. Swap reservation must be performed to reserve space for the `uarea` and its `b_tree` structure. When a new `uarea` is created, its `pregion` is flagged as `PF_NOPAGE` to keep it from being paged by `vhand`. A thread’s `uarea` may be paged but only if the entire process has been marked for deallocation/deactivation during times of extreme memory pressure.

# ## Ready, Set, Run Queue

As soon as all the new kernel structures are created, we are ready to allow the new thread to compete for runtime. We change its `proc` table state to `p_stat`=`SINUSE`, the thread state to `kt_state`=`TSRUN`, and link the `kthread` to the end of the appropriate run queue in accordance with its `kt_spu_wanted` value. We also flag the parent to allow swapping again, as we are through making copies.

In general, a new process and its first thread start on the same `spu` as the parent thread that created it. This makes sense because both initially share the same execution environment and need access to the same text page for their next instruction. See Listing 9.1.