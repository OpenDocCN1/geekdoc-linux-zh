# # Signal Data Structures

Before we get into the process of handling signals, let's look at the associated data structures. Figure 14-1 shows the various signal-related structures and how they relate to the proc and kthread structures.

![](bbox=[0.25, 0.22, 0.78, 0.47])

**Figure 14-1 Signal-Related Data Structures**

With the advent of multithreaded processes in HP-UX version 11.0, the concept of signals became much more complicated, and several new data structures were created. At the same time, much of the data that used to be kept in the proc structure was moved into a new structure called a struct Process_Shared_Fields. The proc structure has a field, p_shared, that points to the Process_Shared_Fields structure. The Process_Shared_Fields is mostly made up of a group of fields of type ksigset_t, which is merely an array of integers used as a bitfield—one bit per signal type. A variety of routines exist in the kernel for manipulating these bitfields—setting or clearing individual bits, setting or clearing all bits, testing bits, and so on. The Process_Shared_Fields structure is shown in Listing 14.1.

# **Listing 14.1 Process_Shared_fields structure**

```
```
struct Process_Shared_Fields {
    ksigset_t pshared_sigignore;   /* signals being ignored */
    ksigset_t pshared_sigcatch;    /* signals being caught by user */
    int       pshared_nsig;        /* # of signals recognized by process */
    void    (*pshared_signal[_NSIG-1])(); /* disposition of signals */
    ksigset_t pshared_sighandmask[_NSIG-1]; /* signals to be blocked */
};
```
```