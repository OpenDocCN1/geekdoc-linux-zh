# Kernel Callout Table

+   * callout_execute() will loop again through the callout table, testing the conditions for function execution. It is possible that another processor took care of things in the interim between function calls and lock releases, so the kernel tests the time values and running flag for the entries in the table before actually executing the function.

+   * Assuming that it is time to run, callout_execute() sets the CALLOUT EXECUTING flag in the callout entry's c_xid field, and the function is invoked.

+   * The callout entry is then removed from the callout table, the structure is placed on the freelist (ct_freelist), and a condition variable is broadcasted if any threads are sleeping on the c_done condition variable. This condition variable is part of the callout entry and provides a method of generating a notification that a function placed on the callout has executed.

The kernel also provides an timeout(9F) interface, which will remove aout.timeout(9F) passed the ID (which was returned from timeout(9F) when the function was placed on the callout table. The entry is located by means of the ctidash[] array and removed, with the callout structure being added to the freelist. Callout entries added by realtime_timeout(9F) can also be removed with timeout(9F). There is no separate function for the removal of real-time callouts.

# 2.5.2 Solaris 2.5.1 Callout Tables

Callout tables in Solaris 2.5.1 are functionally identical to those we described for Solaris 2.6 and Solaris 7; the implementation is different. Solaris 2.5.1 maintains two callout tables—one for normal callouts and one for real-time callouts—which are initialized at boot time. The overall structure of callout tables in Solaris 2.5.1 is illustrated in Figure 2.11.

As you see, many of the structure fields are identical in name (and function) to those described previously. The link to each callout table is made with a callout_state pointer (normal callout table) and an rt callout_state pointer (real-time callout table, not shown in the figure, but identical). The tables implement an array of 256 buckets; each bucket links to a callout structure and maintains the ID for entry.

The initialization process happens at boot time, with two distinct setup phases: one for the normal callout table and one for the real-time callout table. The cs_bucket[] array of the callout_state structure (the callout table, really) is implemented as a circular, singly linked list. At initialization, the b_first pointer is set to point back to itself, and as callouts are added to the bucket, the last-out's c_next will reference the first entry on the bucket. The ID represents a long and short ID name space, as in the Solaris 2.6 and 7 implementations. These fields are set to initial values in each bucket head during the init phase.