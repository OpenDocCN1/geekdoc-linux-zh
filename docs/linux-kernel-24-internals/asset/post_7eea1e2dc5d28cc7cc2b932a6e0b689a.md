
## Non-blocking Semaphore Operations

If SEM_UNDO was asserted for any of the semaphore operations, then the undo list for the current task is searched for an undo structure associated with this semaphore set. During this search, if the semaphore set ID of any of the undo structures is found to be -1, then `freecundos()` is called to free the undo structure and remove it from the list. If no undo structure is found for this semaphore set then `alloc_undo()` is called to allocate and initialize one.

The `try_atomic_semop()` function is called with the `do_undo` parameter equal to 0 in order to execute the sequence of operations. The return value indicates that either the operations passed, failed, or were not executed because they need to block. Each of these cases are further described below:

The `try_atomic_semop()` function returns zero to indicate that all operations in the sequence succeeded. In this case, `update_queue()` is called to traverse the queue of pending semaphore operations for the semaphore set and awaken any sleeping tasks that no longer need to block. This completes the execution of the `sys_semop()` system call for this case.

## Failing Semaphore Operations

If `try_atomic_semop()` returns a negative value, then a failure condition was encountered. In this case, none of the operations have been executed. This occurs when either a semaphore operation would cause an invalid semaphore value, or an operation marked `IPC_NOWAIT` is unable to complete. The error condition is then returned to the caller of `sys_semop()`.

Before `sys_semop()` returns, a call is made to `update_queue()` to traverse the queue of pending semaphore operations for the semaphore set and awaken any sleeping tasks that no longer need to block.

## Blocking Semaphore Operations

The `try_atomic_semop()` function returns 1 to indicate that the sequence of semaphore operations was not executed because one of the semaphores would block. For this case, a new `sem_queue` element is initialized containing these semaphore operations. If any of these operations would alter the state of the semaphore, then the new queue element is added at the tail of the queue. Otherwise, the new queue element is added at the head of the queue.

The `semsleeping` element of the current task is set to indicate that the task is sleeping on this `sem_queue` element. The current task is marked as `TASK_INTERRUPTIBLE`, and the `sleeper` element of the `sem_queue` is set to identify this task as the sleeper. The global semaphore spinlock is then unlocked, and `schedule()` is called to put the current task to sleep.

When awakened, the task re-locks the global semaphore spinlock, determines why it was awakened, and how it should respond. The following cases are handled:

- If the semaphore set has been removed, then the system call fails with `EIDRM`.
- If the `status` element of the `sem_queue` structure is set to 1, then the task was awakened in order to retry the semaphore operations. Another call to `try_atomic_semop()` is made to execute the sequence of semaphore operations. If `try_atomic_semop()` returns 1, then the task must block again as described above. Otherwise, 0 is returned for success, or an appropriate error code is returned in case of failure. Before `sys_semop()` returns, `current->semsleeping` is cleared, and the `sem_queue` is removed from the queue. If any of the specified semaphore operations were altering operations (increase or decrease), then `update_queue()` is called to traverse the queue of pending semaphore operations for the semaphore set and awaken any sleeping tasks that no longer need to block.
- If the `status` element of the `sem_queue` structure is NOT set to 1, and the `sem_queue` element has not been dequeued, then the task was awakened by an interrupt. In this case, the system call fails with `EINTR`. Before returning, `current->semsleeping` is cleared, and the `sem_queue` is removed from the queue. Also, `update_queue()` is called if any of the operations were altering operations.
- If the `status` element of the `sem_queue` structure is NOT set to 1, and the `sem_queue` element has been dequeued, then the semaphore operations have already been executed by `update_queue()`. The queue `status`, which could be 0 for success or a negated error code for failure, becomes the return value of the system call.

## Semaphore Specific Support Structures

The following structures are used specifically for semaphore support:

### struct sem_array

```c
/* One sem_array data structure for each set of semaphores in the system. */
struct sem_array {
    struct kern_ipc_perm sem_perm; /* permissions .. see ipc.h */
    time_t sem_otime; /* last semop time */
    time_t sem_ctime; /* last change time */
    struct sem *sem_base; /* ptr to first semaphore in array */
    struct sem_queue *sem_pending; /* pending operations to be processed */
    struct sem_queue **sem_pending_last; /* last pending operation */
    struct sem_undo *undo; /* undo requests on this array */
    unsigned long sem_nsems; /* no. of semaphores in array */
};
```

### struct sem

```c
/* One semaphore structure for each semaphore in the system. */
struct sem {
    int semval; /* current value */
    int sempid; /* pid of last operation */
};
```

### struct seminfo

```c
struct seminfo {
    int semmap;
    int semmni;
    int semmns;
    int semmnu;
    int semmsl;
    int semopm;
    int semume;
    int semusz;
    int semvmx;
    int semaseg;
};
```

### struct semid64_ds

```c
struct semid64_ds {
    struct ipc64_perm sem_perm; /* permissions .. see ipc.h */
    __kernel_time_t sem_otime; /* last semop time */
    unsigned long __unused1;
    __kernel_time_t sem_ctime; /* last change time */
    unsigned long __unused2;
    unsigned long sem_nsems; /* no. of semaphores in array */
    unsigned long __unused3;
    unsigned long __unused4;
};
```

### struct sem_queue

```c
/* One queue for each sleeping process in the system. */
struct sem_queue {
    struct sem_queue * next; /* next entry in the queue */
    struct sem_queue ** prev; /* previous entry in the queue, * (\n q->prev) == q */
    struct task_struct *sleeper; /* this process */
    struct sem_undo * undo; /* undo structure */
    int pid; /* process id of requesting process */
    int status; /* completion status of operation */
    struct sem_array * sma; /* semaphore array for operations */
    int id; /* internal sem id */
    struct sembuf * sops; /* array of pending operations */
    int nsops; /* number of operations */
    int alter; /* operation will alter semaphore */
};
```

### struct sembuf

```c
/* semop system calls takes an array of these. */
struct sembuf {
    unsigned short sem_num; /* semaphore index in array */
    short sem_op; /* semaphore operation */
    short sem_flg; /* operation flags */
};
```

### struct sem_undo

```c
/* Each task has a list of undo requests. They are executed automatically * when the process exits. */
struct sem_undo {
    struct sem_undo *    proc_next;    /* next entry on this process */
    struct sem_undo *    id_next;      /* next entry on this semaphore set */
    int                  semid;        /* semaphore set identifier */
    short *              semadj;       /* array of adjustments, one per
                                          semaphore */
};
```

## Semaphore Support Functions

The following functions are used specifically in support of semaphores:

### newary()

`newary()` relies on the `ipc_alloc()` function to allocate the memory required for the new semaphore set. It allocates enough memory for the semaphore set descriptor and for each of the semaphores in the set. The allocated memory is cleared, and the address of the first element of the semaphore set descriptor is passed to `ipc_addid()`. `ipc_addid()` reserves an array entry for the new semaphore set descriptor and initializes the `struct kern_ipc_perm` data for the set. The global `used_sems` variable is updated by the number of semaphores in the new set and the initialization of the `struct kern_ipc_perm` data for the new set is completed. Other initialization for this set performed are listed below:

- The `sem_base` element for the set is initialized to the address immediately following the `struct sem_array` portion of the newly allocated data. This corresponds to the location of the first semaphore in the set.
- The `sem_pending` queue is initialized as empty.

All of the operations following the call to `ipc_addid()` are performed while holding the global semaphores spinlock. After unlocking the global semaphores spinlock, `newary()` calls `ipc_buildid()` (via `sem_buildid()`). This function uses the index of the semaphore set descriptor to create a unique ID, that is then returned to the caller of `newary()`.

### freeary()

`freeary()` is called by `semctl_down()` to perform the functions listed below. It is called with the global semaphores spinlock locked and it returns with the spinlock unlocked.

- The `ipc_rmid()` function is called (via the `sem_rmid()` wrapper) to delete the ID for the semaphore set and to retrieve a pointer to the semaphore set.
- The undo list for the semaphore set is invalidated.
- All pending processes are awakened and caused to fail with `EIDRM`.
- The number of used semaphores is reduced by the number of semaphores in the removed set.
- The memory associated with the semaphore set is freed.
