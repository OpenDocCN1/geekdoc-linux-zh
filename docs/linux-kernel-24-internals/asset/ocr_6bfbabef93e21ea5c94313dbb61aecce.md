```
```text
int max_id;
unsigned short seq;
unsigned short seq_max;
struct semaphore sem;
spinlock_t ary;
struct ipc_id* entries;
};
```
```

# struct ipc_id

An array of struct ipc_id exists in each instance of the *ipc_ids* structure. The array is dynamically allocated and may be replaced with larger array by `grow_ary()` as required. The array is sometimes referred to as the descriptor array, since the *kern_ipc_perm* data type is used as the common descriptor data type by the IPC generic functions.

```
```text
struct ipc_id {
struct kern_ipc_perm* p;
};
```
```