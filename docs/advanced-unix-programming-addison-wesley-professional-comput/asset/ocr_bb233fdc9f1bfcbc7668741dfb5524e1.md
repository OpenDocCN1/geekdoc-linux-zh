the underlying memory is the same. As we did before, we'll start with System V shared memory and then move on to POSIX.

# ### 7.13 System V Shared Memory

By now you should be familiar with how the System V IPC calls work. As Section 7.4 explained, you get a key, with `ftok` if you like, and use an `Xget` call (`shmget`) to get an identifier. You control it with an `Xctl` call (`shmtcl`). In the case of shared memory, you attach it to your process with `shmat`, which returns a pointer, and detach it with `shmctl` when you're done with it.

# #### 7.13.1 System V Shared-Memory System Calls

Here are the synopses for the System V shared-memory system calls:

```
**shmget**—get shared memory segment

```c
#include <sys/shm.h>

int shmget(
  key_t key,          /* key */
  size_t size,        /* size of segment */
  int flags           /* creation flags */
);
/* Returns shared-memory identifier or -1 on error (sets errno) */
```
```

```
**shmtcl**—control shared memory segment

```c
#include <sys/shm.h>

int shmtcl(
  int shmid,          /* identifier */
  int cmd,            /* command */
  struct shmld_ds *data /* data for command */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

```
**struct shmld_ds**—structure for `shmtcl`

```c
struct msqid_ds {
  struct ipc_perm shm_perm; /* permission structure */
  size_t shm_segsz;         /* size of segment in bytes */
  pid_t shm_lpid;           /* process ID of last shared memory op */
  pid_t shm_cpid;           /* process ID of creator */
  shmatt_t shm_nattach;     /* number of current attaches */
  time_t shm_atime;         /* time of last shmat */
  time_t shm_dtime;         /* time of last shmdt */
  time_t shm_ctime;         /* time of last change by shmtl */
};
```
```