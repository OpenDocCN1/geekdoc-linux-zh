# Procs - The Process File System

By default, microstate accounting is disabled to keep overhead down to a minimum. Turning microstate accounting on must be done programmatically by means of /proc. The process control file, /proc/<pid>/ctl, must be opened and a control message sent in the form of a write(2) to the control file, which requires an operator (PCSET) and an operand (PR_MSACCT).). Here is a partial code example of how to enable microstate accounting in a process.

```
int control[2];
cfg = /control_file_descriptor */
control[0] = PCSET;
control[1] = PR_MSACCT;
fd = open("/proc/<pid>/ctl", O_WRONLY);
write(fd, control, sizeof(control));
```

Once microstate accounting is enabled, it is reflected in a flag at the process level (SMSACCT in the process structure's p flag) and at the LWP/kthread level (TP MSACCT in the t_proc_flag field). The kernel lwp_create() code tests the process level SMSACCT flag to determine if microstate accounting has been enabled. If it has, lwp_create() sets the SMSACCT flag in the kernel thread. lwp_create() initializes the microstate accounting structure, lwp_mstate, regardless of the state of the SMSACCT flag. This allows the kernel to set the start time (ms_start in the LWP's lwp_mstate structure) and initialize the ms_acct [] array.

The kernel implementation of microstate accounting requires only four kernel functions:

+   - The initialization function init_mstate()
- An update function, new_mstate(), called during state changes
- A function, term_mstate(), to update the process-level data when an LWP terminates
- A function, restore_mstate(), called from the dispatcher when one LWP/kthread has been selected for execution

At various points, the kernel code tests the TP MSACCT flag to determine if microstate accounting is enabled; if it is, the code updates the current microstate by a call to the new_mstate() function, which is passed as an argument flag indicating the new microstate.

The microstates defined by the kernel can be found in /usr/include/sys/msacct.h. They reflect the basic execution states of an LWP/kthread: running, sleeping, or stopped. What they provide is finer-grained information about a particular state, such as when an LWP/kthread was sleeping, what mode it was running in, etc. Table 8-5 describes the microstates, as maintained in the procfs process prisage structure.