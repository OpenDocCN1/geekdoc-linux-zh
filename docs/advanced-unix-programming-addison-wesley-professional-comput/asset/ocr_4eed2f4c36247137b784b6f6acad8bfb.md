# ### 7.10.1 Named POSIX Semaphores

POSIX semaphores are much simpler and much easier to use than System V semaphores. In fact, five of the system calls line right up with the SimpleSem interface from the previous section:

```
**sem_open**—open named semaphore
```
#include <semaphore.h>

sem_t *sem_open(
        const char *name,    /* POSIX IPC name */
        int flags            /* flags (excluding O_CREATE) */
);
/* Returns pointer to semaphore or SEM_FAILED on error (sets errno) */

sem_t *sem_open(
        const char *name,    /* POSIX IPC name */
        int flags,           /* flags (including O_CREATE) */
        mode_t perms,        /* permissions */
        unsigned value       /* initial value */
);
/* Returns pointer to semaphore or SEM_FAILED on error (sets errno) */
```
```

```
**sem_close**—close named semaphore
```
#include <semaphore.h>

int sem_close(
        sem_t *sem           /* semaphore */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

```
**sem_unlink**—remove named semaphore
```
#include <semaphore.h>

int sem_unlink(
        const char *name     /* POSIX IPC name */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

```
**sem_wait**—decrement semaphore
```
#include <semaphore.h>

int sem_wait(
        sem_t *sem           /* semaphore */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```