
## 8.4.1 IPC ID Sequence Numbers

The existence of the sequence number makes it possible to detect the use of a stale IPC ID.

### 8.4.2 IPC Check ID

`ipc_checkid()` divides the given IPC ID by the `SEQ_MULTIPLIER` and compares the quotient with the seq value saved corresponding descriptor. If they are equal, then the IPC ID is considered to be valid and 1 is returned. Otherwise, 0 is returned.

### 8.4.3 Grow Array

`grow_ary()` handles the possibility that the maximum (tunable) number of IDs for a given IPC type can be dynamically changed. It enforces the current maximum limit so that it is no greater than the permanent system limit (`IPCMNI`) and adjusts it down if necessary. It also insures that the existing descriptor array is large enough. If the existing array size is sufficiently large, then the current maximum limit is returned. Otherwise, a new larger array is allocated, the old array is copied into the new array, and the old array is freed. The corresponding global spinlock is held when updating the descriptor array for the given IPC type.

### 8.4.4 Find Key

`ipc_findkey()` searches through the descriptor array of the specified `ipc_ids` object, and searches for the specified key. Once found, the index of the corresponding descriptor is returned. If the key is not found, then -1 is returned.

### 8.4.5 Check Permissions

`ipcperms()` checks the user, group, and other permissions for access to the IPC resources. It returns 0 if permission is granted and -1 otherwise.

### 8.4.6 Lock

`ipc_lock()` takes an IPC ID as one of its parameters. It locks the global spinlock for the given IPC type, and returns a pointer to the descriptor corresponding to the specified IPC ID.

### 8.4.7 Unlock

`ipc_unlock()` releases the global spinlock for the indicated IPC type.

### 8.4.8 Lock All

`ipc_lockall()` locks the global spinlock for the given IPC mechanism (i.e., shared memory, semaphores, and messaging).

### 8.4.9 Unlock All

`ipc_unlockall()` unlocks the global spinlock for the given IPC mechanism (i.e., shared memory, semaphores, and messaging).

## 8.5 Generic IPC Get/Parse Functions

### 8.5.1 ipc_get()

`ipc_get()` takes a pointer to a particular IPC type (i.e., shared memory, semaphores, or message queues) and a descriptor ID, and returns a pointer to the corresponding IPC descriptor. Note that although the descriptors for each IPC type are of different data types, the common `kern_ipc_perm` structure type is embedded as the first entity in every case. The `ipc_get()` function returns this common data type. The expected model is that `ipc_get()` is called through a wrapper function (e.g., `shm_get()`) which casts the data type to the correct descriptor data type.

### 8.5.2 ipc_parse_version()

`ipc_parse_version()` removes the `IPC_64` flag from the command if it is present and returns either `IPC_64` or `IPC_OLD`.

## 8.6 Generic IPC Structures used with Semaphores, Messages, and Shared Memory

The semaphores, messages, and shared memory mechanisms all make use of the following common structures:

### 8.6.1 struct kern_ipc_perm

Each of the IPC descriptors has a data object of this type as the first element. This makes it possible to access any descriptor from any of the generic IPC functions using a pointer of this data type.

```c
/* used by in-kernel data structures */
struct kern_ipc_perm {
    key_t key;
    uid_t uid;
    gid_t gid;
    uid_t cuid;
    gid_t cgid;
    mode_t mode;
    unsigned long seq;
};
```

### 8.6.2 struct ipc_ids

The `ipc_ids` structure describes the common data for semaphores, message queues, and shared memory. There are three global instances of this data structure—`semids_ds`, `msgids_ds` and `shmid_ds`—for semaphores, messages and shared memory respectively. In each instance, the `sem` semaphore is used to protect access to the structure. The `entries` field points to an IPC descriptor array, and the `ary` spinlock protects access to this array. The `seq` field is a global sequence number which will be incremented when a new IPC resource is created.

```c
struct ipc_ids {
    int size;
    int in_use;
    int max_id;
    unsigned short seq;
    unsigned short seq_max;
    struct semaphore sem;
    spinlock_t ary;
    struct ipc_id* entries;
};
```

### 8.6.3 struct ipc_id

An array of `struct ipc_id` exists in each instance of the *ipc_ids* structure. The array is dynamically allocated and may be replaced with larger array by `grow_ary()` as required. The array is sometimes referred to as the descriptor array, since the *kern_ipc_perm* data type is used as the common descriptor data type by the IPC generic functions.

```c
struct ipc_id {
    struct kern_ipc_perm* p;
};
```
