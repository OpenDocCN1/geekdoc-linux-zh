```
**pthread_mutex_lock**—lock mutex

```c
#include <pthread.h>

int pthread_mutex_lock(
        pthread_mutex_t *mutex    /* mutex to lock */
);
/* Returns 0 on success, error number on error */
```
```

```
**pthread_mutex_unlock**—unlock mutex

```c
#include <pthread.h>

int pthread_mutex_unlock(
        pthread_mutex_t *mutex    /* mutex to unlock */
);
/* Returns 0 on success, error number on error */
```
```

Mutual exclusion works like this: If a mutex is already locked, **pthread_mutex_lock** blocks until it is unlocked.

The simplest way to get a suitable mutex variable is just to declare it with an initializer, like this:

```
`static pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;`
```

It can be local to the file (*static*) or shared between files (*extern*). You can also have mutexes on the stack (automatic variables) or allocated dynamically, but then you need to initialize them with a call to **pthread_mutex_init**, which I won't detail here.$^{21}$

Now we can modify our example to adequately protect the shared data:

```
```c
static pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;
static long x = 0;

static void *thread_func(void *arg)
{
    bool done;

    while (true) {
        ec_rv( pthread_mutex_lock(&mtx) )
        done = x >= (long)arg;
        ec_rv( pthread_mutex_unlock(&mtx) )
```
```