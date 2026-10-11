```
for(j = 0; j < maxthreads; j++) {
if(threads[j].exists) {
threadWait(&threads[j].thrd);
threads[j].exists = 0;
threads[j].active = 0;
nexists--;
vsema(&availableThreads);
}
}
}
```

These three modules require some background discussion. The listener module simply accepts new sockets and queues them. It is simple, and the only thing to think about is that it must queue the work consistently; therefore, it uses the enqueue() routine. The thread scheduler must create threads or allocate existing (pooled) threads. Threads are created with a pthread_create() call. Because our program wants to start a thread that is either already created (a pooled thread) or create a fresh one, we have chosen to abstract the thread-starting process with the threadStart() routine. tThreadStart() uses the pooling global variable to determine whether to use a pooled thread or to simply start a new thread. The pooling global defaults to no pooling and is a command-line option.

The command line tells the server and client how many threads to use. The default is one. The server runs no more than the number of threads specified on the command line at one time. This works in the same way for the client. Each server thread performs its work and ends. A pooled thread ends by marking itself as inactive and blocking on a lock. An unpooled thread simply returns, thus destroying the thread. For nonpooled threads, the cleanup routine is essential if the system is not to run out of resources. It is the cleanup routine that returns the resources used by nonpooled threads to the system.

We add one further observation about our thread code. Writing threaded code that schedules work using pooled threads is not exactly trivial. Determining why things are not working properly can be time-consuming. We demonstrate here one method of making the debugging task simpler. Our thread management routines (scheduler and cleanup) each have a global state variable. The state variables represent the current state of the routine and are accessible from all threads in the program. The variables are changed just prior to any function call that could block. By printing these two state variables, we can determine exactly where in the code the scheduler and cleanup threads are currently blocked. We wrote a trivial debug thread that can print the values of these state variables, and together with the state variables the debugging task was significantly accelerated.

# ## Synchronization

The scheduler uses synchronization primitives (semaphores) to block when there is nothing to do. Semaphores are used as a synchronized counting mechanism where,