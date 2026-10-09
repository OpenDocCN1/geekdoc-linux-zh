# **Return Value**

Always zero.

# **Parameters**

+   * `mutex` The mutex to create or destroy.
* `mutexattr` Any attributes to set. If NULL, the call uses the default setting (`PTHREAD_MUTEX_INITIALIZER`).

# **Possible Errors**

(none)

+   * `pthread_mutex_lock()`, `pthread_mutex_trylock()`

Lock or try to lock a semaphore for entering a critical section. The parameter is simply a variable that acts like a reservation ticket. If another thread tries to lock a reserved spot, it blocks until the reserving thread releases the semaphore.

# **Prototype**

```
```
#include <pthread.h>
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
```
```

# **Return Value**

The call returns zero on success and nonzero on error. You can find the exact code in `errno`.

# **Parameter**

| Parameter | Description |
| :--- | :--- |
| `mutex` | The semaphore variable |

# **Possible Errors**

| Error | Description |
| :--- | :--- |
| `EINVAL` | The mutex has not been properly initialized. |
| `EDEADLK` | (`pthread_mutex_try_lock`) The calling thread has already locked the mutex (error-checking mutexes only). |
| `EBUSY` | (`pthread_mutex_lock`) The calling thread can't acquire because it is currently locked. |

# **Example**

```
```
pthread_mutex_t mutex = fastmutex;
...
if ( pthread_mutex_lock(&mutex) == 0 )
{
    /**** work on critical data ****/
    pthread_mutex_unlock(&mutex);
}
```
```