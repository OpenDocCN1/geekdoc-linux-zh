Table 10.6 Semaphore Methods (continued)

| Method | Description |
| :----- | :------- |
| down_interruptible (struct semaphore *) | Tries to acquire the given semaphore and enter interruptible sleep if it is contended |
| down (struct semaphore *) | Tries to acquire the given semaphore and enter uninterruptible sleep if it is contended |
| down_trylock (struct semaphore *) | Tries to acquire the given semaphore and immediately return nonzero if it is contended |
| up (struct semaphore *) | Releases the given semaphore and wakes a waiting task, if any |

# # Reader-Writer Semaphores

Semaphores, like spin locks, also come in a reader–writer flavor. The situations where reader–writer semaphores are preferred over standard semaphores are the same as with reader–writer spin locks versus standard spin locks.

Reader–writer semaphores are represented by the `struct rw_semaphore` type, which is declared in `<linux/rwsem.h>`. Statically declared reader–writer semaphores are created via the following, where name is the declared name of the new semaphore:

```
static DECLARE_RWSEM(name);
```

Reader–writer semaphores created dynamically are initialized via

```
init_rwsem(struct rw_semaphore *sem)
```

All reader–writer semaphores are mutexes—that is, their usage count is one—although they enforce mutual exclusion only for writers, not readers. Any number of readers can concurrently hold the read lock, so long as there are no writers. Conversely, only a sole writer (with no readers) can acquire the write variant of the lock. All reader–writer locks use uninterruptible sleep, so there is only one version of each down(). For example:

```
static DECLARE_RWSEM (mr_rwsem);

/* attempt to acquire the semaphore for reading ... */
down_read (&mr_rwsem);

/* critical region (read only) ... */

/* release the semaphore */
up_read (&mr_rwsem);
```