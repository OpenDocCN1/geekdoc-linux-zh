# semctl_down()

semctl_down() provides the `IPC_RMID` and `IPC_SET` operations of the semctl() system call. The semaphore set ID and the access permissions are verified prior to either of these operations, and in either case, the global semaphore spinlock is held throughout the operation.

# IPC_RMID

The IPC_RMID operation calls `freary()` to remove the semaphore set.

# IPC_SET

The IPC_SET operation updates the `uid`, `gid`, `mode`, and `ctime` elements of the semaphore set.

# semctl_nolock()

semctl_nolock() is called by `sys_semctl()` to perform the IPC_INFO, SEM_INFO and SEM_STAT functions.

# IPC_INFO and SEM_INFO

IPC_INFO and SEM_INFO cause a temporary `seminfo` buffer to be initialized and loaded with unchanging semaphore statistical data. Then, while holding the global `sem_ids.sem` kernel semaphore, the `semusz` and `semaem` elements of the `seminfo` structure are updated according to the given command (IPC_INFO or SEM_INFO). The return value of the system call is set to the maximum semaphore set ID.

# SEM_STAT

SEM_STAT causes a temporary `semid64_ds` buffer to be initialized. The global semaphore spinlock is then held while copying the `sem_otime`, `sem_ctime`, and `sem_nsems` values into the buffer. This data is then copied to user space.

# semctl_main()

semctl_main() is called by `sys_semctl()` to perform many of the supported functions, as described in the subsections below. Prior to performing any of the following operations, semctl_main() locks the global semaphore spinlock and validates the semaphore set ID and the permissions. The spinlock is released before returning.

# GETALL

The GETALL operation loads the current semaphore values into a temporary kernel buffer and copies them out to user space. The small stack buffer is used if the semaphore set is small. Otherwise, the spinlock is temporarily dropped in order to allocate a larger buffer. The spinlock is held while copying the semaphore values in to the temporary buffer.

# SETALL

The SETALL operation copies semaphore values from user space into a temporary buffer, and then into the