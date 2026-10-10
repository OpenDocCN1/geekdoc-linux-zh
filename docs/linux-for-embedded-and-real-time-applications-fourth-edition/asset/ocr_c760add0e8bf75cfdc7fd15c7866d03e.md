![](bbox=[0.2, 0.05, 0.85, 0.35])

What is needed is some way to regulate access to the printer, so that only one task can use it at a time.

A *mutex* (short for “mutual exclusion”) acts like a key to control access to a resource. Only the thread that has the key can use the resource. In order to use the resource (in this case a printer), a thread must first *acquire* the key (mutex) by calling an appropriate kernel service (Fig. 9.2). If the key is available, that is the resource (printer) is not currently in use by someone else, the thread is allowed to proceed. Following its use of the printer, the thread releases the mutex so another thread may use it.

If, however, the printer is in use, the thread is blocked until the thread that currently has the mutex releases it. Any number of threads may try to acquire the mutex while it is in use. All of them will be blocked. The waiting threads are queued, either in order of priority or in the order in which they called pthread_mutex_lock(). The choice of how threads are queued at the mutex may be built into the kernel, or it may be a configuration option when the mutex is created.

```
```c
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

int pthread_mutex_init (pthread_mutex_t *mutex, const pthread_mutexattr_t *mutex_attr);
int pthread_mutex_destroy (pthread_mutex_t *mutex);

int pthread_mutex_lock (pthread_mutex_t *mutex);
int pthread_mutex_unlock (pthread_mutex_t *mutex);
int pthread_mutex_trylock (pthread_mutex_t *mutex);
```
```