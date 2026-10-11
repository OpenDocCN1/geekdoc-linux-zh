# # Locking

The primary advantage of using threads is sharing data memory. Because the threads may try to revise the memory at the same time, you need to lock the memory for exclusive access. This section describes *pthread* calls that you can use (even with clones) to lock memory.

# ## pthread_mutex_init(), pthread_mutex_destroy()

These calls create and destroy mutex semaphore variables. You may not need the initializer because the defined variables are easier and faster to use. The destroy call normally frees up any resources. However, the Linux implementation uses no allocated resources, so the call does nothing more than check whether the resource is unlocked.

**Prototype**

```
```
#include <pthread.h>
```
```

```
```
/*---Predefined mutex settings---*/
pthread_mutex_t fastmutex = PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t recmutex = PTHREAD_RECURSIVE_MUTEX_INITIALIZER_NP;
pthread_mutex_t errchkmutex = PTHREAD_ERRORCHECK_MUTEX_INITIALIZER_NP;

int pthread_mutex_init(pthread_mutex_t *mutex,
 const pthread_mutexattr_t *mutexattr);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```
```

**Return Value**

Always zero.

**Parameters**

+   *   mutex
+       The mutex to create or destroy.
+   *   mutexattr
+       Any attributes to set. If *NULL*, the call uses the default setting (*PTHREAD_MUTEX_INITIALIZER*).

**Possible Errors**

(none)

# ## pthread_mutex_lock(), pthread_mutex_trylock()

Lock or try to lock a semaphore for entering a critical section. The parameter is simply a variable that acts like a reservation ticket. If another thread tries to lock a reserved spot, it blocks until the reserving thread releases the semaphore.

**Prototype**

```
```
#include <pthread.h>
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
```
```