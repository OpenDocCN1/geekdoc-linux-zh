
```c
if ((key = ftok(name, 1)) == -1) {
    if (errno != ENOENT)
        EC_FAIL
} else {
    if ((semid = semget(key, 1, PERM_FILE)) == -1) {
        if (errno != ENOENT)
            EC_FAIL
    } else
        ec_negl(semctl(semid, 0, IPC_RMID));
}
return true;
EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

Now, back to System V. We’re ready to introduce the scary `semop` system call, which does both `semwait` and `sempost` operations:

### semop—operate on semaphore set
```c
#include <sys/sem.h>

int semop(
    int semid,                  /* identifier */
    struct sembuf *sops,        /* operations */
    size_t nsops                /* number of operations */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

### struct sembuf—structure for semop
```c
struct sembuf {
    unsigned short sem_num;     /* semaphore number */
    short sem_op;               /* Semaphore operation */
    short sem_flg;              /* Operation flags */
};
```

As I said, `semop` doesn’t just operate on one semaphore but on as many as you like, even the whole set. You need to build an array of operations (`struct sembufs`) before you make the call, although if there’s only one to be operated on, a single `struct sembuf` will do—you just pass its address and use 1 for `nsops`.

Each `sem_op` can be positive, negative, or zero:

- **> 0** The value of `sem_op` is added to the semaphore value (*sempost*).
- **< 0** The absolute value of `sem_op` is subtracted from the value, unless that would make the value go negative, in which case the call blocks until the entire value can be subtracted (*semwait*).
- **0** The call blocks until the value becomes zero.

All of the operations passed to `semop` are performed atomically, and the function doesn't return until everything is done. (Unless it's interrupted by thread cancellation, a signal, or the removal of the semaphore set.)

You can prevent blocking by setting the `SEM_UNDO` flag in the `sem_flg` member for an operation. If any operation in the array would block and has the flag set, `semop` returns immediately. Because `semop` always acts atomically, no other operations are done, even if they appeared earlier in the array and even if they wouldn't have blocked.

There's one more feature: For every semaphore that a process increments or decrements, an adjustment is kept, along with the actual value. When the `SEM_UNDO` flag is set for an incrementing operation, the adjustment is decremented, and vice versa for a decrementing operation. When a process exits, its adjustment is added to the semaphore's value, thus undoing whatever the process did to the semaphore. For example, suppose a process decrements a semaphore (i.e., *semwait*) to lock a buffer, and increments it (*sempost*) when it's done. With the `SEM_UNDO` flag, it can ensure that the buffer is unlocked if it should exit abnormally.

For our simple semaphores, we only want to operate on one at a time, we only increment or decrement by 1, and we don't use `SEM_UNDO`. So `SimpleSemWait` and `SimpleSemPost` are, well, simple:

### SimpleSemWait—decrement simple semaphore
```c
#include "SimpleSem.h"

bool SimpleSemWait(
    struct SimpleSem *sem    /* semaphore */
);
/* Returns true on success or false on error (sets errno) */
```

### SimpleSemPost—increment simple semaphore
```c
#include "SimpleSem.h"

bool SimpleSemPost(
    struct SimpleSem *sem    /* semaphore */
);
/* Returns true on success or false on error (sets errno) */
```

Here’s the code:

```c
bool SimpleSemWait(struct SimpleSem *sem)
{
    struct sembuf sop;

    sop.sem_num = 0;
    sop.sem_op = -1;
    sop.sem_flg = 0;
    ec_negl( semop(sem->sm_sm_semId, &sop, 1) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemPost(struct SimpleSem *sem)
{
    struct sembuf sop;

    sop.sem_num = 0;
    sop.sem_op = 1;
    sop.sem_flg = 0;
    ec_negl( semop(sem->sm_sm_semId, &sop, 1) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

I should mention one additional use of System V semaphores before we move on: to pass an integer between processes. Suppose, for example, a client wants to pass its process ID to a server. It gets access to a semaphore and sets its value to its process ID. Then the server can look at the value to get the number. Since a semaphore set can have an array of semaphores, you can pass an array of integers this way.

## 7.10 POSIX Semaphores

These semaphore system calls are part of the POSIX standard, though optional, and you have to check the `_POSIX_SEMAPHORES` feature-test macro to tell whether they’re present (see Section 1.5.4 and Section 7.6.3). As of now, they’re not in FreeBSD, Darwin, or Linux.

### 7.10.1 Named POSIX Semaphores

POSIX semaphores are much simpler and much easier to use than System V semaphores. In fact, five of the system calls line right up with the SimpleSem interface from the previous section:

### sem_open—open named semaphore
```c
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

### sem_close—close named semaphore
```c
#include <semaphore.h>

int sem_close(
    sem_t *sem           /* semaphore */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

### sem_unlink—remove named semaphore
```c
#include <semaphore.h>

int sem_unlink(
    const char *name     /* POSIX IPC name */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

### sem_wait—decrement semaphore
```c
#include <semaphore.h>

int sem_wait(
    sem_t *sem           /* semaphore */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

### sem_post—increment semaphore
```c
#include <semaphore.h>

int sem_post(
    sem_t *sem           /* semaphore */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

POSIX semaphores are counting semaphores, like System V variants, but in steps of one only. Each `sem_t` object represents only one semaphore, not a set of them, as with System V.

The calls for opening, closing, and unlinking follow the pattern for POSIX IPC calls that we saw in Section 7.7.1 for POSIX message-queue system calls. In particular, the name passed to `sem_open` has to follow the portability rules that were discussed in Section 7.6.2. As you would expect, `sem_post` adds one to the semaphore’s value, and `sem_wait` subtracts one, blocking if the value is already zero.

You don’t use `O_RDONLY`, `O_WRONLY`, or `O_RDWR` with `sem_open`, as they’re meaningless—the semaphore is useless unless `sem_post` and `sem_wait` can both be used.

All the initialization rigmarole that we needed for System V is gone. We just pass the value we want (often zero) to `sem_open`.

Be careful about the return value from `sem_open` when it fails: It’s `SEM_FAILED`, not `NULL`, which is the usual failure return from functions that otherwise return a pointer.

The implementation of the SimpleSem calls for POSIX semaphores is trivial:

```c
struct SimpleSem *SimpleSemOpen(const char *name)
{
    struct SimpleSem *sem = NULL;

    ec_null( sem = malloc(sizeof(struct SimpleSem)) );
    if ((sem->sm_sem = sem_open(name, O_CREAT, PERM_FILE, 0)) == SEM_FAILED)
        EC_FAIL;
    return sem;

EC_CLEANUP_BGN
    free(sem);
    return NULL;
EC_CLEANUP_END
}

bool SimpleSemClose(struct SimpleSem *sem)
{
    ec_neg1( sem_close(sem->sm_sm_sem) );
    free(sem);
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemRemove(const char *name)
{
    if (sem_unlink(name) == -1 && errno != ENOENT)
        EC_FAIL;
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemPost(struct SimpleSem *sem)
{
    ec_neg1( sem_post(sem->sm_sm_sem) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemWait(struct SimpleSem *sem)
{
    ec_neg1( sem_wait(sem->sm_sm_sem) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

10. If you’re not familiar with this term, one dictionary I consulted defined it as “a complicated, petty set of procedures,” which is just perfect.
