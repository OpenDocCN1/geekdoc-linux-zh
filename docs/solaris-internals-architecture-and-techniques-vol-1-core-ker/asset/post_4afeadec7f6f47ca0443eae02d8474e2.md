
# Solaris Doors 465

- The kernel door_call() code (nothing happens at the doors library level) in door_call() allocates a door_data structure from kernel memory and links it to the t_door pointer in the calling kernel thread.
- If a pointer to an argument structure (door_arg) was passed in the door_call(3), the arguments are copied from the passed structure in user space to the door_arg structure embedded in door_data.
- If no arguments were passed, the door_arg fields are zeroed and the d_results flag in door_data is set to indicate no results can be returned.

The door_call(3) API defines that a NULL argument pointer means no results can be returned. A lookup is performed on the passed door descriptor and returns a pointer to the door_node. Typically, file descriptor lookup return a vnode pointer. In this case, the vnode pointer and the door_node pointer are one the same because the vnode is embedded in the door_node, located at the top of the structure.

- The kernel door_get_server() function retrieves a server kernel thread from the pool to execute the function.
- The thread is removed from the list of available server threads (p_server_threads) and changed from TS_SLEEP to TS_ONPROC state (this thread was sleeping on a shuttle object, not sitting on a sleep queue).
- The arguments from the caller are copied to the server thread returned from door_get_server(). The door_active counter in the door_node is incremented, the calling (client) thread's d_error field in door_data is set to DOOR_WAIT, the server thread's d_call field (door_data structure for the server thread) is set to the client (caller), and a pointer to the door_node is set in the server thread's door_data active field.

With the necessary data fields set, control can be transferred to the server thread; this transfer is done with a call to shuffle_resume().

- shuffle_resume() is passed a pointer to the server thread removed from the pool.

Just to get back to focus for a moment (in you're lost among the trees), we enter into shuffle_resume() as a result of a kernel thread issuing door_call(3). The door_call() kernel code up to this point essentially allocates or initialized the necessary data structures for the server thread to have the exported function on behalf of the caller. The shuffle_resume() function is entered from door_call(), so the kernel now executing in shuffle_resume() is the client door. So, what needs to happen is pretty simple (relatively speaking)—the server thread, which was passed to shuffle_resume() as an argument—to get control of the processor, and the current thread executing the shuttle_resume() code needs to be put to sleep on a shuttle object, since the current thread and the client thread are one and the same. So:

- shuttle_resume() sets up the current thread to sleep on a shuttle object in the same manner described previously (t_wchan0 set to 1, state set to TS_SLEEP, etc.); the server thread has its T_WAKEABLE flag, t_wchan0 field, and t_wobj_ops field cleared.
- The code tests for any interesting events that may require attention, such as a hold condition on the thread, and checks for posted signals. If any signals are posted, setrun() is called with the current (client) thread.
- Finally, the dispatcher switch_to_to() function is called and is passed the server thread address. switch_to() updates the per-processor context-switch counter in the cpu_sysinfo structure (pswitch) and calls resume() to have the server thread context-switched onto the processor. The general flow is illustrated in Figure 10.8.

![](img/a86367b95bf21add858c99948ac951c6_511_0.png)

# Figure 10.8 door_call() Flow with Shuttle Switching

- The server thread executes the function associated with the server_node, as specified by the first argument passed when the server executed door_create(3).
- The last call by the server function door_return(3), which returns results and control to the calling thread (client) and blocks in the server, waiting for another door_call(3).

# Solaris Doors

 467

- The kernel door_return() code copies the return data back to the caller and places the server thread in the door server pool. The calling (client) thread, which we left in a sleep state back in door_call(), is set back to an T_ONPROC state, and the shuttle code (shuttle_resume()) is called to give the processor back to the caller and have it resume execution.

Some final points to make regarding doors. There's a fair amount of code in the kernel doorfs module designed to deal with error conditions and the premature termination of the calling thread or server thread. In general, if the calling thread is awakened early, that is, before door_call() has completed, the code figures out why the wakeup occurred (signal, exit call, etc.) and sends a cancel signal (SIGCANCEL) to the server thread. If a server thread is interrupted because of a signal, exit, error condition, etc., the door_call() code bails out. In the client, an EINTR (interrupted system call) error will be set, signifying that door_call() terminated prematurely.
