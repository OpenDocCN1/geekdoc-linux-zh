door_return(3X) is part of the doors API and is typically called at the end of the function being exported by the door_create(3X) call.

+   - `door_return(3X)` returns processor control to the thread that issued `door_call(3X)` and causes the server thread to sleep, waiting for another invocation of the door function.
+   - When entered (remember, we’re in the kernel now, not in the doors library), `door_return()` allocates a `door_data` structure for the calling thread and links it to the kernel thread’s `t_door` pointer. This sequence is done if the current thread’s `t_door` pointer is NULL, signifying a `door_data` structure has not yet been allocated.

The next bit of code in `door_return()` applies to argument handling, return data, and other conditions that need to be dealt with when a kernel thread issues `door_call(3X)`. We’re still in the door create phase, so a bit later we’ll revisit what happens in `door_return()` as a result of `door_call(3X)`.

Continuing with the door create in the `door_return()` kernel function:

+   - The kernel `door_release_server()` code is called to place the current thread on the list of threads available to execute on behalf of door calls into the server.
+   - The kernel thread is linked to the process’s `p_server_thread` link, and `cv_broadcast()` is done on the door condition variable, `door_cv`, causing any threads blocked in `door_call(3X)` to wake up.
+   - At this point, the door create is essentially completed.
+   - A call into the shuttle code to place the kernel thread to sleep on a shuttle synchronization object is made (`shuttle_swtch()`); the thread is thus placed in a sleep state and enters the dispatcher through `swtch()`.

We now digress slightly to explain shuttle synchronization objects. Typically, execution control flow is managed by the kernel dispatcher (Chapter 5), using condition variables and sleep queues. Other synchronization primitives, mutex locks, and reader/writer locks are managed by turnstiles, an implementation of sleep queues that provides a priority inheritance mechanism.

Shuttle objects are a relatively new (introduced in Solaris 2.5, when doors first shipped) synchronization object that essentially allows very fast transfer of control of a processor from one kernel thread to another without incurring the overhead of the dispatcher queue searching and normal kernel thread processing. In the case of a `door_call()`, control can be transferred directly from the caller (or client in this case), to a thread in the door server pool, which executes the door function on behalf of the caller. When the door function has completed, control is transferred directly back to the client (caller), all using the kernel shuttle interfaces to set thread state and to enter the dispatcher at the appropriate places. This direct transfer of processor control contributes significantly to the IPC perfor-