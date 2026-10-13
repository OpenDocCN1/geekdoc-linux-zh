# Table 8-10  *siginfo Structure*  *(Continued)*

| Structure or Union | Field Name | Data Type | Description |
|---|---|---|---|
|  | `nsysarg` | `char` | number of sys call args |
|  | `fault` | `char` | last fault code |

At the process level, there are three `k_sigset_t` structures (see Figure 8.22 on page 332):

+   - The `p_sig` field has a bit set for each signal pending for the process
+   - `p_ignore` represents signals with the disposition set to ignore
+   - `p_siginfo` indicates there is information in a `siginfo` structure about the signal.

The `siginfo` data structure is embedded in the `siqueue` structure, a linked list of which is rooted in the process `p_siqueue` pointer for any signals queued to the process. `siqueue` structures are allocated from a pool pointed to by `p_sqhgrd`. The pool of `siqueue` structures is allocated the first time a `siqueue(2)` system call is executed by the process. Thirty-two (the default) `siqueue` structures are linked to form the available pool. An additional pool is rooted at the `p_sigqnhdr` for signotify calls. (The `signotify(2)` system call is not currently exposed as an API in Solaris—it’s used internally from within the POSIX message queue facility.) Signals that have reached the notification phase—they’ve been generated but not yet delivered—are represented in the `p_notifsigs` field, along with a condition variable, `p_notifcv`, for synchronization between the aswap and the process.

In the embedded `uarea`, several bit maps are maintained for flagging various signal-related events or forcing a particular behavior, settable by the `sigaction(2)` system call. An array of pointers exists to signal dispositions: `u_signal[MAXSIG]`, which contains one array entry per signal. The entries in the array may indicate the signal is to be ignored (`SIG_IGN`) or the default action is set (`SIG_DEF`). If the signal is to be caught, with a handler installed by `signal(3C)` or `sigaction(2), the array location for the signal points to the function to be invoked when the signal is delivered. The `uarea` signal fields are described in the following list. The described behavior occurs when a signal corresponding to a bit that is set in the field is posted.

+   - `u_sigonstack` — Flags an alternate signal stack for handling the signal. Assumes `sigaltstack(2)` has been called to set up an alternate stack. If one has not been set up, the signal is handled on the default stack. Set by `sigaction(2)`, with the `SA_ONSTACK` flag in `sa_flags` field of `sigaction` structure.
+   - `u_sigresethand` — Resets the disposition to default (`SIG_DEF`) when the handler is entered for the signal. The signal will not be blocked when the handler is entered. As above, set by `SA_RESETHAND` in `sa_flags`.