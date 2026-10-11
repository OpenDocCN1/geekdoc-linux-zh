```
// Send 'Q'
tp->cbuf[0] = 'Q';
rc = Send(sock, (char *)tp->cbuf, 1, 0);
if(rc != 1) {
    printf("\ tCLIENT[%d]: Send 'Q' FAILED: rc=%d err=%d\ n",
           th,rc,Errno);
    fflush(stdout);
    exit(1);
}
tp->sndbytes += 1;
rc = CLOSESOCK(sock);
if(rc != 0) {
    printf("\ tCLIENT[%d]: close socket %d FAILED: Errno=%d\ n",
           th,sock,Errno);
    exit(1);
}
```

# Code Discussion

A number of different synchronization mechanisms have been used here. Counting semaphores are used to simply count available resources. The counter blocks when none is available. Both the thread scheduler and cleanup thread use a semaphore to know when something needs to be done. An earlier cleanup design simply looked for active threads every 2 seconds. Although the performance difference is probably negligible, the resulting design using semaphores leaves the system completely idle when there is nothing to do. (psema, vsema, and initsema are based on Posix semaphores.)

Locking primitives are used to count the number of work items in the client. They are based on a memory variable and a critical section lock. This design was developed from the queuing primitives described in the next paragraph. The desire to queue millions of items suggested that each should take no memory. Therefore, this interface was derived to support decrementing a counter as the mechanism for dequeuing an object. (initck, lck, and unlock are based on Posix thread mutexes.)

Finally, the third version of synchronization used is to queue objects. A Posix pthread mutex is used to guard an actual memory queue, each element of which can contain a single integer. The integer in our case is a socket file descriptor received from the listen_and_connect() routine in the server's main thread. (initq, enqueue, and dequeue are based on the previously described locking primitives, which in turn are based on Posix thread mutexes.)

Our design is asynchronous. The server consumes no CPU cycles if there is nothing to do. The client either has something to do or it exits. The client's responsibility is to pass all the work to be done to the server, wait until the server completes all the work, and finally print timing and performance results.