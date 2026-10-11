
while(connect(sock2, (struct sockaddr *)&addr1,
                sizeof(addr1))) {
    int err;

    err = Errno;
    if(err != ECONNREFUSED) {
        printf("connect FAILED: err=%d\n", Errno);
        exit(1);
    }
    SLEEP(2); // Be polite
    *per_client_refusecnt++;
    if(refusedcount++ >= econnrefuseretries) {
        printf("connect FAILED: ");
        printf("after %d ECONNREFUSED attempts\n",
                econnrefuseretries);
        exit(1);
    }
}
    return sock2;
}

These two code segments bear some discussion. The `listen_and_accept()` routine is written to be used as simply as possible; it either returns a usable socket or prints an error and exits. The `clientconnect()` routine either returns a usable socket or prints an error and exits. It processes the ECONNREFUSED error return in an attempt to deal with a server that is too busy to accept the socket request. That happens to any `listen` and `accept` loop when the queue of requests in the operating system is longer than the default of 5. For instance, if a server issues a `listen_and_accept()`, receives an incoming socket, and then simply goes to sleep, succeeding incoming requests are queued by the operating system until there are five of them. The sixth connection request is refused, and the ECONNREFUSED error is reported by the client issuing a connect request (`clientconnect()` in our case). Our code simply sleeps for 2 seconds and tries again. We have allowed, by default, four retries. The number can be changed by editing the program and recompiling. Alternatively, it would be trivial to add a new option that allows the value to be set on the command line.

We have described the actions required to create socket connections. The details of socket connections are seldom the source of performance problems. It is what happens after the socket is created that becomes interesting.

## Threads

Because our program uses threads and demonstrates thread pooling, we must describe how threads work and our usage of them. We don’t claim that any of the following code is the best-performing code. We do claim that the code demonstrates how threads can be used in both a pooled and nonpooled manner, and that the code is reasonably good. No doubt, improvements are possible.

Recalling from earlier, our description of the server *main* program where a scheduler and a cleanup thread were created, we will show these two modules. There is a third module we haven't yet mentioned. It is the thread that listens for new work to queue. The work is the newly created socket, and it is the socket that is queued. Our worker program reads a text string from the socket containing the file size and block size to use in doing the work. Other experimentations with this code could replace our worker thread with one written for almost any purpose whatever. To summarize, the following takes place:

- 1. The Listener listens for new connections and inserts work (the newly created socket) into the work queue.
- 2. The thread scheduler waits for work in the queue and starts a thread passing the socket file descriptor to the thread. The scheduler can be run using *pooled* threads or in the mode where it creates a new thread for each work item (-*pooling* command-line option).
- 3. The work thread does all the work and finally closes the socket.
- 4. The thread cleanup awaits thread deaths and cleans up after them.

Surrounding the worker thread are the fixtures to report back to the client the completion of the task.

The thread listener is coded as shown here:

```c
void ServerMain()
{
    SOCKTYPE sock;

    initq(&workq);
    newThread( (void(*)(void *)) threadScheduler,0, &schedulerT);
    newThread( (void(*)(void *)) threadCleanup,0, &cleanupT);
    newThread( (void(*)(void *)) threadDbg, 0, &dbgT);

    // Server waits in a listen/accept sequence and hands off
    // request to a thread. Threads are either dynamically
    // created or there is a pool.
    //
    // listen_and_accept creates sockets
    //
    for(;;) {
        listen_and_accept(&sock);
        enqueue(&workq, sock);
        vsema(&workq.sema);
    }
}
```

The thread scheduler reads information from a queue. The queue is protected by synchronization primitives, which we discuss later in the chapter. The protections allow multiple threads to update the queue without making the queue metadata inconsistent. The thread scheduler is coded as shown here:

```c
void threadScheduler()
{
  SOCKTYPE sock;
  int rc;

  //
  // threadScheduler decrements availableThreads,
  // threadCleanup  increments availableThreads.
  //
  for(;;) {

    schedulerstate = 1;
    psema(&workq.sema);

    schedulerstate = 2;
    psema(&availableThreads);

    schedulerstate = 3;
    if (dequeue(&workq, (int *)&sock)) {
      schedulerstate = 4;
      rc = threadStart(sock); // starting a thread
      if (rc == -1) {
        printf("threadStart FAILED: maxthreads=%d\n",
               maxthreads); fflush(stdout);
        exit(1);
      }
    }
    else {
      printf("Workq Sema count wrong\n");
      exit(1);
    }
  }
}
```

Thread cleanup is coded as shown here:

```c
void threadCleanup()
{
  int j = 0;

  //
  // For pooled threads, this loop will last forever.
  //
  for(;;) {
    cleanupstate = 1;
    psema(&ActiveT);
    cleanupstate = 2;

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
}
```

These three modules require some background discussion. The listener module simply accepts new sockets and queues them. It is simple, and the only thing to think about is that it must queue the work consistently; therefore, it uses the enqueue() routine. The thread scheduler must create threads or allocate existing (pooled) threads. Threads are created with a pthread_create() call. Because our program wants to start a thread that is either already created (a pooled thread) or create a fresh one, we have chosen to abstract the thread-starting process with the threadStart() routine. threadStart() uses the pooling global variable to determine whether to use a pooled thread or to simply start a new thread. The pooling global defaults to no pooling and is a command-line option.

The command line tells the server and client how many threads to use. The default is one. The server runs no more than the number of threads specified on the command line at one time. This works in the same way for the client. Each server thread performs its work and ends. A pooled thread ends by marking itself as inactive and blocking on a lock. An unpooled thread simply returns, thus destroying the thread. For nonpooled threads, the cleanup routine is essential if the system is not to run out of resources. It is the cleanup routine that returns the resources used by nonpooled threads to the system.

We add one further observation about our thread code. Writing threaded code that schedules work using pooled threads is not exactly trivial. Determining why things are not working properly can be time-consuming. We demonstrate here one method of making the debugging task simpler. Our thread management routines (scheduler and cleanup) each have a global state variable. The state variables represent the current state of the routine and are accessible from all threads in the program. The variables are changed just prior to any function call that could block. By printing these two state variables, we can determine exactly where in the code the scheduler and cleanup threads are currently blocked. We wrote a trivial debug thread that can print the values of these state variables, and together with the state variables the debugging task was significantly accelerated.

## Synchronization

The scheduler uses synchronization primitives (semaphores) to block when there is nothing to do. Semaphores are used as a synchronized counting mechanism where, if there are things to do, the number of things to do is reflected in the value of the semaphore. If the count is greater than zero, the psema() routine decrements the count by one and returns to the calling program. If the value of the semaphore is zero, the psema() routine blocks. The vsema() operation increments the semaphore and never blocks. Our psema() and vsema() routines are based on the semaphores(3) interfaces defined in section 3 of the manual (man 3 semaphores). Our interfaces take a name that enables us to debug them with more clarity—we can print the name of the semaphore we are examining by inserting appropriate print statements. We use one semaphore to count the number of available threads (either pooled or nonpooled), one to count the number of tasks (jobs, work items, or whatever we want to call them), and one to count the number of active threads.

The semaphore interfaces are defined as shown here:

```c
void initsema(PVSEMA *s, int initvalue, int hi, char *name)
{
 if(sem_init(&s->pv,0,initvalue) == -1) {
 printf("sem_init() FAILED: sema=<%s> err=%d\n",name,Errno);
 exit(1);
 }
 s->name = name;
}
void psema(PVSEMA *s) // decrements or blocks if s==0
{
 sem_wait(&s->pv);
}
void vsema(PVSEMA *s) // increments
{
 int rc;

 rc = sem_post(&s->pv);
 if(rc == -1) {
 printf("sem_post(<%s>) FAILED: err=%d\n",name,Errno);
 exit(1);
 }
}
```

Finally, there are the queueing operations. Their job is to protect the data structures describing the queue of jobs coming in. The queue is operated with enqueue() and dequeue() operations. To support the queueing and dequeueing of data, lock and unlock implement locks on specified objects (the work queue in this case). We will show the enqueue routine and the associated dequeue routine.

You might ask why there are two counting mechanisms. The semaphore counting mechanism is specifically for counting. Because the numbers of threads (active and available) are strictly numbers, the only mechanism we need is counting. The queueing routines were written for more general queueing where objects could be queued. In this case, they require more than a simple count. For our particular demonstration here, they have been tailored to queue only integers (socket file descriptors); thus, they are similar in function to the semaphore operations.
