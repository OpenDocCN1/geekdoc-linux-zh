
the underlying memory is the same. As we did before, we'll start with System V shared memory and then move on to POSIX.

## 7.13 System V Shared Memory

By now you should be familiar with how the System V IPC calls work. As Section 7.4 explained, you get a key, with `ftok` if you like, and use an `Xget` call (`shmget`) to get an identifier. You control it with an `Xctl` call (`shmctl`). In the case of shared memory, you attach it to your process with `shmat`, which returns a pointer, and detach it with `shmdt` when you're done with it.

### 7.13.1 System V Shared-Memory System Calls

Here are the synopses for the System V shared-memory system calls:

**`shmget`**—get shared memory segment

```c
#include <sys/shm.h>

int shmget(
  key_t key,          /* key */
  size_t size,        /* size of segment */
  int flags           /* creation flags */
);
/* Returns shared-memory identifier or -1 on error (sets errno) */
```

**`shmctl`**—control shared memory segment

```c
#include <sys/shm.h>

int shmctl(
  int shmid,          /* identifier */
  int cmd,            /* command */
  struct shm_ds *data /* data for command */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

**`struct shm_ds`**—structure for `shmctl`

```c
struct shm_ds {
  struct ipc_perm shm_perm; /* permission structure */
  size_t shm_segsz;         /* size of segment in bytes */
  pid_t shm_lpid;           /* process ID of last shared memory op */
  pid_t shm_cpid;           /* process ID of creator */
  shmatt_t shm_nattach;     /* number of current attaches */
  time_t shm_atime;         /* time of last shmat */
  time_t shm_dtime;         /* time of last shmdt */
  time_t shm_ctime;         /* time of last change by shmctl */
};
```

**`shmat`**—attach shared memory segment

```c
#include <sys/shm.h>

void *shmat(
 int shmid, /* identifier */
 const void *shmaddr, /* desired address or NULL */
 int flags /* attachment flags */
);

/* Returns pointer or -1 on error (sets errno) */
```

**`shmdt`**—detach shared memory segment

```c
#include <sys/shm.h>

int shmdt(
 const void *shmaddr /* pointer to segment */
);

/* Returns 0 on success or -1 on error (sets errno) */
```

As you’d expect, `shmget` accesses a shared memory segment, creating it if necessary and if the `IPC_CREAT` or `IPC_PRIVATE` flags are present. The `size` argument is meaningful only if the segment is created. A newly created segment is initialized to zeros.

Then, to use the segment, you call `shmat`, which gives you a pointer to it. Oddly, `shmat` returns −1 on an error, not `NULL`. This works because it will never return a pointer that can be mistaken for −1; in fact, returned pointers are even numbers on essentially all UNIX systems.

When you’re done with the segment, you call `shmdt`, passing in the pointer you got from `shmat`, not the identifier. The segment stays around until it’s explicitly removed (via `shmctl` or the `ipc(1)` command) or until the machine is rebooted, so you’re free to reattach it. You might get a different pointer, though.

Normally, you don’t care what address `shmat` gives you, so you set the second argument to `NULL`. But, if you want, you can try to force it to give you the address you specify with `shmaddr`. If it can’t, because that address is already in use or otherwise invalid, it fails with `errno` set to `EINVAL`. There’s also a flag, `SHM_RND`, for rounding the address to a proper boundary, but I won’t describe the details. Another flag, `SHM_RDONLY`, if set, attaches the segment read-only.

With `shmctl` you use the same commands as with the other `Xctl` system calls, `IPC_STAT`, `IPC_SET`, and `IPC_RMID`. `IPC_SET` sets `shm_perm.uid`, `shm_perm.gid`, and the low-order 9 bits of `shm_perm.mode`.

Here’s a simple program that shows how a segment (a small one!) can be shared between two processes:

```c
static int *getaddr(void)
{
    key_t key;
    int shmfd, *p;

    (void)close(open("shmeeg", O_WRONLY | O_CREAT, 0));
    ec_negl( key = ftok("shmeeg", 1) )
    ec_negl( shmfd = shmget(key, sizeof(int), IPC_CREAT | PERM_FILE) )
    ec_negl( p = shmat(shmfd, NULL, 0) )
    return p;

    EC_CLEANUP_BGN
        return NULL;
    EC_CLEANUP_END
}

int main(void)
{
    pid_t pid;

    if ((pid = fork()) == 0) {
        int *p, prev = 0;

        ec_null( p = getaddr() )
        while (*p != 99)
            if (prev != *p) {
                printf("child saw %d\n", *p);
                prev = *p;
            }
        printf("child is done\n");
    }
    else {
        int *p;

        ec_null( p = getaddr() )
        for (*p = 1; *p < 4; (*p)++)
            sleep(1);
        *p = 99;
    }

    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

Each process calls `getaddr`; one of them creates the segment, and the other just accesses it. Here’s the output we got:

```
$ shmem
child saw 1
child saw 2
child saw 3
$ child saw 99
child is done
```

A little strange, no? Why did the child report that it saw 99 when that’s what terminates its `while` loop? Well, in the line

```c
while (*p != 99)
```

`*p` was equal to 3 at one point, but by the time it got to the line

```c
printf(“child saw %d\n”, *p);
```

`*p` was already 99. (The `$` prompt is where it is because the parent didn’t wait for the child before exiting. That’s not a defect but a pretty common occurrence in UNIX.)

Things get even stranger if you run `shmem` a second time:

```
$ shmem
child is done
$
```

It broke! No, actually all that’s wrong is that the segment was left there—unattached—after `shmem` terminated the first time, and it still held the value 99. In the second execution, the child saw 99 before the parent even got to its `for` loop. Obviously, we could fix this problem by removing the segment when `shmem` terminates. But you get the point: Sharing memory is tricky!

### 7.13.2 Shared Memory and Semaphores

The example in the previous section is wrong for another, more subtle reason: As we saw with threads (Section 5.17.3), we can’t assume that references to `*p` are atomic. Generally, you can’t share memory between processes without some control in the form of a semaphore. Therefore, let’s add that in (`getaddr` is unchanged):

```c
int main(void)
{
    pid_t pid;

    ec_false( SimpleSemRemove("shmxsem") )
    if ((pid = fork()) == 0) {
        struct SimpleSem *sem;
        int *p, prev = 0, n;

        ec_null( sem = SimpleSemOpen("shmxsem") )
        ec_null( p = getaddr() )
        while (true) {
            ec_false( SimpleSemWait(sem) )
            n = *p;
            ec_false( SimpleSemPost(sem) )
            if (n == 99)
                break;
            if (prev != n) {
                printf("child saw %d\n", n);
                prev = n;
            }
        }
        printf("child is done\n");
        ec_false( SimpleSemClose(sem) )
    }
    else {
        struct SimpleSem *sem;
        int *p, i;

        ec_null( sem = SimpleSemOpen("shmxsem") )
        ec_null( p = getaddr() )
        *p = 0;
        ec_false( SimpleSemPost(sem) )
        for (i = 1; i < 4; i++) {
            ec_false( SimpleSemWait(sem) )
            *p = i;
            ec_false( SimpleSemPost(sem) )
            sleep(1);
        }
        ec_false( SimpleSemWait(sem) )
        *p = 99;
        ec_false( SimpleSemPost(sem) )
        ec_false( SimpleSemClose(sem) )
    }

    exit(EXIT_SUCCESS);
}

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
```

Here’s the output now—it’s much more sensible:

```
$ shmex2
child saw 1
child saw 2
child saw 3
$ child is done
shmex2
child saw 1
child saw 2
child saw 3
$ child is done
```

Look at all the changes we needed to put in the protection:

- The child assigned `*p` to local memory with the semaphore locked and then was free to use the local memory with the semaphore unlocked.
- Similarly, the parent used a local variable in the `for` loop, locking the semaphore only to access the shared memory.
- Initially, the semaphore is locked (zero value), so the parent is free to initialize the shared memory to zero. Then it calls `SimpleSemPost` to get things moving. It’s OK if the child accesses the shared memory at that point. This version then can be run repeatedly since it initializes the segment each time it’s run.
- We remove the semaphore at the start of each run so that it will start with zero.

Although we’ve fixed the atomicity problems, the child process is still inefficient. To see why, look again at its loop:

```c
while (true) {
    ec_false( SimpleSemWait(sem) )
    n = *p;
    ec_false( SimpleSemPost(sem) )
    if (n == 99)
        break;
    if (prev != n) {
        printf("child saw %d\n", n);
        prev = n;
    }
}
```

It keeps racing around and around, locking and unlocking the semaphore, but only does something (prints) when the value changes. Most of its efforts are wasted, and all the locking keeps the semaphore unavailable for no reason. Wouldn’t it be better for the parent to just tell the child when the value changed? (This is reminiscent of the motivation for condition variables in Section 5.17.4.)
