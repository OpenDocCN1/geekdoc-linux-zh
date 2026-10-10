
Before an attribute object can be used, it must be initialized. Then, any of the attributes defined for that object may be set or retrieved with the appropriate functions. This must be done before the attribute object is used in a call to `pthread_create()`. If necessary, an attribute object can also be “destroyed”. Note that a single attribute object can be used in the creation of multiple threads.

The only required attribute for thread objects is the “detach state”. This determines whether or not a thread can be joined when it terminates. The default detach state is `PTHREAD_CREATE_JOINABLE`, meaning that the thread can be joined on termination. The alternative is `PTHREAD_CREATE_DETACHED`, which means the thread cannot be joined.

Joining is useful if you need the thread’s return value, or you want to make sure threads terminate in a specific order. Otherwise, it is better to create the thread detached. The resources of a joinable thread cannot be recovered until another thread joins it, whereas a detached thread’s resources can be recovered as soon as it terminates.

There are also a number of optional scheduling policy attributes.

## **Synchronization: Mutexes**

As soon as we introduce a second independent thread of execution, we create the potential for resource conflicts. Consider the somewhat contrived example of two threads, each of which wants to print the message “I am Thread $n$” on a single shared printer, as shown in Fig. 9.1. In the absence of any kind of synchronizing mechanism, the result could be something like “Il a mm TaTasskk 12”.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_152_0.png)

```
Code in Thread n
`printf("I am thread %d\n", thread);`
```

**Figure 9.1**
Resource conflict.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_153_0.png)

What is needed is some way to regulate access to the printer, so that only one task can use it at a time.

A *mutex* (short for “mutual exclusion”) acts like a key to control access to a resource. Only the thread that has the key can use the resource. In order to use the resource (in this case a printer), a thread must first *acquire* the key (mutex) by calling an appropriate kernel service (Fig. 9.2). If the key is available, that is the resource (printer) is not currently in use by someone else, the thread is allowed to proceed. Following its use of the printer, the thread releases the mutex so another thread may use it.

If, however, the printer is in use, the thread is blocked until the thread that currently has the mutex releases it. Any number of threads may try to acquire the mutex while it is in use. All of them will be blocked. The waiting threads are queued, either in order of priority or in the order in which they called `pthread_mutex_lock()`. The choice of how threads are queued at the mutex may be built into the kernel, or it may be a configuration option when the mutex is created.

```c
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

int pthread_mutex_init (pthread_mutex_t *mutex, const pthread_mutexattr_t *mutex_attr);
int pthread_mutex_destroy (pthread_mutex_t *mutex);

int pthread_mutex_lock (pthread_mutex_t *mutex);
int pthread_mutex_unlock (pthread_mutex_t *mutex);
int pthread_mutex_trylock (pthread_mutex_t *mutex);
```

The Pthreads mutex API follows much the same pattern as the thread API. There is a pair of functions to initialize and destroy mutex objects, and a set of functions to act on the mutex objects. The listing also shows an alternate way to initialize statically allocated mutex objects. `PTHREAD_MUTEX_INITIALIZER` provides the same default values as `pthread_mutex_init()`.

Two operations may be performed on a mutex: lock and unlock. The lock operation causes the calling thread to block if the mutex is not available. There is another function called `trylock` that allows you to test the state of a mutex without blocking. If the mutex is available, `trylock` returns success and locks the mutex. If the mutex is not available, it returns `EBUSY`.

### Mutex Attributes

Mutex attributes follow the same basic pattern as thread attributes. There is a pair of functions to create and destroy a mutex attribute object. We will defer discussion of the `pshared` attribute until later. There are some other attributes we will take up shortly.

The mutex “attribute” type actually started out as a Linux nonportable extension to Pthreads. The Pthreads standard explicitly allows nonportable extensions. The only requirement is that any symbol that is nonportable must have “_np” appended to its name.

Mutex type was subsequently incorporated into the Pthreads standard.

```c
int pthread_mutexattr_init (pthread_mutexattr_t *attr);
int pthread_mutexattr_destroy (pthread_mutexattr_t *attr);

int pthread_mutexattr_gettype (pthread_mutexattr_t *attr, int *type);
int pthread_mutexattr_settype (pthread_mutexattr_t *attr, int type);

type =  PTHREAD_MUTEX_NORMAL
        PTHREAD_MUTEX_ERRORCHECK
        PTHREAD_MUTEX_RECURSIVE
        PTHREAD_MUTEX_DEFAULT

int pthread_mutexattr_getprioceiling (const pthread_mutexattr_t *mutex_attr, int *prioceiling);
int pthread_mutexattr_setprioceiling (pthread_mutexattr_t *mutex_attr, int prioceiling);
```

```c
int pthread_mutexattr_getprotocol (pthread_mutexattr_t *mutex_attr, int *protocol);

int pthread_mutexattr_setprotocol (pthread_mutexattr_t *mutex_attr, int protocol);

int pthread_mutexattr_getprioceiling (const pthread_mutexattr_t *mutex_attr, int *prioceiling);

int pthread_mutexattr_setprioceiling (pthread_mutexattr_t *mutex_attr, int prioceiling);

protocol = PTHREAD_PRIO_NONE
           PTHREAD_PRIO_INHERIT
           PTHREAD_PRIO_PROTECT
```

What happens if a thread should attempt to lock a mutex that it has already locked? Normally the thread would simply hang up. The “type” attribute alters the behavior of a mutex when a thread attempts to lock a mutex that it has already locked. The possible values for type are:

- **Normal.** If a thread attempts to lock a mutex it already holds, it is blocked and thus effectively deadlocked. The normal mutex does no consistency or sanity checking.
- **Error checking.** If a thread attempts to recursively lock an error checking mutex, the lock function returns immediately with the error code `EDEADLK`, meaning you cannot do this because you have already locked the mutex. Furthermore, the unlock function returns an error if it is called by a thread other than the current owner of the mutex.
- **Recursive.** A recursive mutex allows a thread to successfully lock a mutex multiple times. It counts the number of times the mutex was locked, and requires the same number of calls to the unlock function before the mutex goes to the unlocked state. This type also checks that the mutex is being unlocked by the same thread that locked it.
- **Default.** The standard says that this type results in “undefined behavior” if a recursive lock is attempted. It also says that an implementation may map Default to one of the other types.

Optionally, a Pthreads mutex can implement the priority inheritance or priority ceiling protocols to avoid priority inversion. The mutex attribute `protocol` can be set to “none”, “priority inheritance”, or “priority ceiling”, represented by the symbol `PTHREAD_PRIO_PROTECT`. The `prioceiling` attribute sets the value for the priority ceiling.

## **Problems With Solving the Resource Sharing Problem: Priority Inversion**

Using mutexes to resolve resource conflicts can lead to subtle performance problems. Consider the scenario illustrated in Fig. 9.3. Threads 1 and 2 each require access to a common resource protected by a mutex. Thread 1 has the highest priority, and Thread 2 has the lowest. Thread 3, which has no need for the resource, has a “middle” priority.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_156_0.png)

**Figure 9.3**
Priority inversion scenario.

**Fig. 9.4** is an execution timeline of this system. Assume Thread 2 is currently executing and pends on the mutex. The resource is free, so Thread 2 gets it. Next, an interrupt occurs that makes Thread 1 ready. Since Thread 1 has higher priority, it preempts Thread 2, and executes until it pends on the *resource* mutex.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_156_1.png)

**Figure 9.4**
Execution timeline.

Since the resource is held by Thread 2, Thread 1 blocks, and Thread 2 regains control. So far everything is working as we would expect. Even though Thread 1 has higher priority, it simply has to wait until Thread 2 is finished with the resource.

The problem arises if Thread 3 should become ready while Thread 2 has the resource locked. Thread 3 preempts Thread 2. This situation is called *priority inversion*, because a lower priority thread (Thread 3) is effectively preventing a higher priority thread (Thread 1) from executing.
