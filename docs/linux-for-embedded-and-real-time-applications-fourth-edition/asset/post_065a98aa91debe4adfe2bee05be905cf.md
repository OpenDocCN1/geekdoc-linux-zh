
A common solution to this problem is to temporarily raise the priority of Thread 2 to that of Thread 1 as soon as Thread 1 pends on the mutex. Now, Thread 2 cannot be preempted by anything of lower priority than Thread 1. This is called priority inheritance.

Another approach, called priority ceiling, raises the priority of Thread 2 to a specified value higher than that of any task that may pend on the mutex as soon as Thread 2 gets the mutex. This is considered to be more efficient, because it eliminates unnecessary context switches. No thread needing the resource can preempt the thread currently holding it.

Posix threads has optional attributes for setting a mutex’s protocol as either priority inheritance or priority ceiling, and for setting the priority ceiling value.

## Communication: Condition Variables

There are many situations where one thread needs to notify another thread about a change in status to a shared resource protected by a mutex. Consider the situation in Fig. 9.5, where two threads share access to a queue. Thread 1 reads the queue and Thread 2 writes it. Clearly, each thread requires exclusive access to the queue, and so we protect it with a mutex.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_157_0.png)

Thread 1 will lock the mutex and then see if the queue has any data. If it does, Thread 1 reads the data, and unlocks the mutex. However, if the queue is empty, Thread 1 needs to block somewhere until Thread 2 writes some data. Thread 1 must unlock the mutex before blocking, or else Thread 2 would not be able to write. But there is a gap between the time Thread 1 unlocks the mutex and blocks. During that time, Thread 2 may execute and not recognize that anyone is blocking on the queue.

The condition variable solves this problem by waiting (blocking) with the mutex locked. Internally, the conditional wait function unlocks the mutex, allowing Thread 2 to proceed. When the conditional wait returns, the mutex is again locked.

```c
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

int pthread_cond_init (pthread_cond_t *cond, const pthread_condattr_t *cond_attr);
int pthread_cond_destroy (pthread_cond_t *cond);

int pthread_cond_wait (pthread_cond_t *cond, pthread_mutex_t *mutex);
int pthread_cond_timedwait (pthread_cond_t *cond, pthread_mutex_t *mutex, const struct timespec *abstime);
int pthread_cond_signal (pthread_cond_t *cond);
int pthread_cond_broadcast (pthread_cond_t *cond);
```

The basic operations on a condition variable are *signal* and *wait*. Signal wakes up one of the threads waiting on the condition. The order in which threads wake up is a function of scheduling policy. A thread may also execute a *timed wait*, such that if the specified time interval expires before the condition is signaled, the wait returns with an error. A thread may also *broadcast* a condition. This wakes up all threads waiting on the condition.

## Condition Variable Attributes

Pthreads does not define any required attributes for condition variables, although there is at least one optional attribute.

## Thread Termination and Cancellation

A thread may be terminated either voluntarily or involuntarily. A thread terminates itself either by simply returning, or by calling `pthread_exit()`. In the latter case, all *cleanup handlers* that the thread registered by calls to `pthread_cleanup_push()` are called prior to termination.

Most threads run in an infinite loop. As long as the system is powered up, the thread is running, doing its thing. Some threads start up, do their job, and finish. But there are also circumstances where it is useful to allow one thread to terminate another thread involuntarily. Perhaps the user presses a CANCEL button to stop a long search operation. Maybe the thread is part of a redundant numerical algorithm, and is no longer needed because another thread has solved the problem. The Pthreads cancellation mechanism provides for the orderly shutdown of threads that are no longer needed.

But cancellation must be done with care. You do not just arbitrarily stop a thread at any point in its execution. Suppose it has a mutex locked. If you terminate a thread that has locked a mutex, it can never be unlocked. The thread may have allocated one or more dynamic memory blocks. How does that memory get returned if the thread is terminated?

Pthreads allows each thread to manage its own termination, such that the thread can free up and/or return any global resources before it actually terminates. So, when you cancel a thread you are usually not stopping it immediately, you are asking it to terminate itself as soon as it is safe or convenient.

Pthreads supports three cancellation modes (Fig. 9.6) encoded as two bits called *cancellation state* and *cancellation type*. A thread may choose to disable cancellation because it is performing an operation that must be completed. The default mode is Deferred, meaning that cancellation can only occur at specific points, called *cancellation points*, where the program tests whether the thread has been requested to terminate. Most functions that can block for an unbounded time, such as waiting on a condition variable or reading or writing a file, are cancellation points, and are defined as such in the Posix specification.

| Mode | State | Type | Meaning |
| :--- | :--- | :--- | :--- |
| Off | Disabled | N/A | Cancellation remains pending until enabled |
| Deferred | Enabled | Deferred | Cancellation occurs at next cancellation point |
| Asynchronous | Enabled | Asynchronous | Cancellation may occur at any time |

**Figure 9.6**

Cancellation modes.

While asynchronous cancellation mode might seem like a good idea, it is rarely safe to use. That is because, by definition, you do not know what state the thread is in when it gets the cancellation request. It may have just called `pthread_mutex_lock()`. Is the mutex locked? Don’t know. So while asynchronous cancellation mode is in effect, you cannot safely acquire any shared resources.

```c
int pthread_cancel (pthread_t thread);
int pthread_setcancelstate (int state, int *oldstate);
int pthread_setcanceltype (int type, int *oldtype);
void pthread_testcancel (void);
```

A thread can cancel another thread by calling `pthread_cancel()`. `pthread_setcancelstate()` and `pthread_setcanceltype()` allow a thread to set its cancellation mode. Note that these functions return the previous value of state and type respectively. The function `pthread_testcancel()` allows you to create your own cancellation points. It returns immediately if the thread has not been requested to terminate. Otherwise, it does not return.

## Cleanup Handlers

When a thread is requested to terminate itself, there may be some things that need to be “cleaned up” before the thread can safely terminate. It may need to unlock a mutex, or return a dynamically allocated memory buffer, for example. That is the role of *cleanup handlers*. Every thread conceptually has a stack of active cleanup handlers. Handlers are pushed on the stack by `pthread_cleanup_push()`, and executed in reverse order when the thread is cancelled or calls `pthread_exit()`. A cleanup handler takes one `void *` argument.

```c
void pthread_cleanup_push (void (*routine)(void *), void *arg);
void pthread_cleanup_pop (int execute);
```

The most recently pushed cleanup handler can be popped off the stack with `pthread_cleanup_pop()` when it is no longer needed. Often, the functionality of a cleanup handler is needed whether or not the thread terminates. The execute argument specifies whether or not a handler is executed when it is popped. A nonzero value means execute. Note also that `pthread_cleanup_pop()` can only be called from the same function that called `pthread_cleanup_push()`. Aside from being good programming practice, this is necessary because `pthread_cleanup_push()` is a macro that, in many implementations, ends with an opening brace, “{”; introducing a block of code, `pthread_cleanup_pop()` then has the corresponding closing brace.

*Listing 9.2* shows the read thread (the main function) of a typical queueing application with a cleanup handler added. We assume the default deferred cancellation mode. Note that `pthread_cleanup_pop()` is used to unlock the mutex, rather than the normal mutex unlock function.

The reason we need a cleanup handler here is that `pthread_cond_wait()` is a cancellation point, and the mutex is locked when we call it. But is it really necessary to push and pop the cleanup handler on every pass through the while loop? It is if there is a cancellation point in the section called “do something with the data” where the mutex is unlocked. This thread can only invoke the cleanup handler if it has the mutex locked. If there are no cancellation points while the mutex is unlocked, then it is safe to move the push cleanup call outside the loop. In that case, we do not really need pop cleanup.

We will have an opportunity to use a cleanup handler in the next chapter.
