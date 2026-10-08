the process via the kill signal (SIGKILL). If the process is nonexistent, ignore the entry.

+   - **once**
When boot init enters a run level that matches the entry's rstate, start the process and do not wait for its termination. When it dies, do not restart the process. If boot init enters a new run level but the process is still running from a previous run level change, the process is not restarted.

+   - **ondemand**
This instruction is really a synonym for the respawn action. It is functionally identical to respawn but is given a different keyword in order to divorce its association with run levels. This is used only with the a, b, or c values described in the rstate field.

+   - **powerfail**
Execute the process associated with this entry only when boot init receives a power-fail signal (SIGPWR; see signal(5)).

+   - **powerwait**
Execute the process associated with this entry only when boot init receives a power-fail signal (SIGPWR) and wait until it terminates before continuing any processing of inittab.

+   - **respawn**
If the process does not exist, start the process; do not wait for its termination (continue scanning the inittab file). When it dies, restart the process. If the process currently exists, do nothing and continue scanning the inittab file.

+   - **sysinit**
Entries of this type are executed before boot init tries to access the console. It is expected that this entry will be only used to initialize devices on which boot init might attempt to obtain run level information. These entries are executed and waited for before continuing.

+   - **wait**
When boot init enters the run level that matches the entry's rstate, start the process and wait for its termination. Any subsequent reads of the inittab file while boot init is in the same run level cause boot init to ignore this entry.

+   - **process**
This is a sh command to be executed. The entire process field is prefixed with exec and passed to a forked sh as "sh -c 'exec command". For this reason,