# # Features Of Use Of Semaphores

Semaphores can be used to solution ' Liabilities synchronize two different tasks.

+   1. With their help, it is possible to organize mutual exclusion (to protect the code of critical sections from execution by more than one thread). It is most convenient to use a **binary semaphore**, which can take two values: 0 and 1. Here is an example of implementing a critical section using a binary semaphore:

```
```c
semaphore _ t sem = 1; // at the beginning the semaphore is open
down (sem);
// critical section
up (here);
```
```

+   2. With their help, you can organize the expectation of the fulfillment of some condition. Suppose that one needs to organize the wait for one thread to complete another (analog of the join operation). In this case, a semaphore with an initial value of 0 (closed) can be used. The stream that is waiting must perform a down operation for this semaphore and in order to signal the completion of the stream, its completion function requires up to perform the same semaphore. Here is the pseuodocode (this_thread stands for current thread):

```
```c
Void thread_init ()
{
    this _ thread. sem = 0; // At the beginning of the stream
    execution the semaphore is exposed
}
void thread _ exit ()
{
```
```