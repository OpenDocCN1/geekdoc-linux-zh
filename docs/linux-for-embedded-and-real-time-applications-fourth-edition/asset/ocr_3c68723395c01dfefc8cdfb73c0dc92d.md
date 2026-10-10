when creating the monitor. The structure should probably also include the socket number. It is this “meta” `pthread_t` object that gets allocated and passed to the monitor thread.

Now the question is, when can the flag be set to the “free” state? Again, the monitor cannot do it, because the `pthread_t` object is still in use until the thread actually exits. Here is where the third state, PENDING, comes in.

The monitor sets the flag to PENDING just before it terminates. Then we create a separate thread, call it “resource” if you will, that does the following:

+   1. Wakes up periodically and checks for monitor threads that have set their flags to PENDING
+   2. Joins the thread
+   3. Marks the meta pthread object free
+   4. Goes back to sleep

Remember that when one thread joins another, the “joiner” (in this case resource) is blocked until the “joinee” (monitor) terminates. So, when resource continues from the `pthread_join()` call, the just-terminated monitor’s `pthread_t` object is guaranteed to be free. The semantics of `pthread_join()` are:

```
```c
int pthread_join (pthread_t thread, void **ret_value)
```
```

It is quite likely that by the time the resource thread wakes up, the monitor thread has already exited, in which case `pthread_join()` returns immediately with the error code `ESRCH`, meaning that `thread` does not exist.

The `createThread()` function now needs to create the server thread and the resource thread. Likewise, `terminateThread()` needs to cancel and join both of those. And of course, any monitor threads that are running also need to be cancelled. That is, when the resource thread terminates, it needs to go through the list of meta pthreads checking for running monitors. Ah, but the resource thread doesn’t know it is being cancelled.

Here is a good use for a cleanup handler. Write a cleanup handler that runs through the list of meta pthreads looking for any that are in the IN USE state. Cancel and join the corresponding thread. Call `pthread_cleanup_push()` just before the main loop in the resource thread. Add a call to `pthread_cleanup_pop()` just after the loop. It will never be called, but it closes the block opened by `pthread_cleanup_push()`.

If you do not feel up to writing this yourself, you may have already noticed that there is an implementation of `multimon.c` in the `samples./working/` directory.

There is a separate makefile called `Makefile.multi` to build the multiple client versions of `netthermo`. The build command for the Eclipse target is:

```
```
make -f Makefile.multi
```
```