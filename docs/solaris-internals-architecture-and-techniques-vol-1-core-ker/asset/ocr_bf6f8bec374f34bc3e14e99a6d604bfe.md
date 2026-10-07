# Table 8-5 Microstates

| prusage Field | Flag | Description |
|---|---|---|
| pr_utime | LMS_USER | User mode execution time. |
| pr_stime | LMS_SYSTEM | System (kernel) mode execution time. |
| pr_ttime | LMS_TRAP | Other system trap time (other meaning aside from system calls, which are accounted for in pr_stime). |
| pr_ftptime | LMS_TFAULT | Time sleeping while waiting for a page fault on a text page to be resolved. |
| pr_dftime | LMS_DEFAULT | Time sleeping while waiting for a page fault on a data page to be resolved. |
| pr_kftime | LMS_KFAULT | Time sleeping while waiting for a kernel page fault to be resolved. |
| pr_ltime | LMS_USER_LOCK | Time sleeping while waiting for a user lock (e.g., user-defined mutex lock). |
| pr_slptime | LMS_SLEEP | Any sleep time not accounted for in the above fields. |
| pr_wtime | LMS_WAIT_CPU | Time spent waiting for an available CPU. |
| pr_stoptime | LMS_STOPPED | Time spent (e.g., job control or debugging). |

The microstate measurements are taken as follows: init mstate initializes the microstate date of new LWP/kthread when the LWP/kthread is created. The init_mstate() function performs the following actions (see the previous page).

+   - Set the previous microstate, ms_prev, to LMS_SYSTEM.
- Set ms_start to return the value of the getrhtime() call.
- Set ms_state_start to return the value of getrhtime() call.
- Set t_mstate in the kernel thread to LMS_STOPPED.
- Set Zero the msacct ([] array).

The LWP/kthread microstate data is thus initialized prior to executing the first time. The above initialization steps show two microstate-related fields not discussed. In the thread structure, the current microstate is maintained in t_mstate, and t_waitrq calculates CPU wait time. We will see where this comes from in a moment later.

During execution if TP_MSACCT is set, calls are made to the new_mstate() routine when a state transition occurs. The caller passes new_mstate() a state flag (LMS_USER, LMS_SYSTEM, etc.) that stipulates the new state. The system calculates the time spent in the previous state by finding the difference between the current value of getrhtime() and the ms_state_start field, which was