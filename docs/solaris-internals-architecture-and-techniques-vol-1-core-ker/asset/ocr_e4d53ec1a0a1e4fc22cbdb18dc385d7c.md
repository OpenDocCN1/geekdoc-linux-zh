# Interprocess Communication

The kernel ipcget() routine is invoked from each of the IPC xxxget(2) system calls; its behavior is determined by whether the object already exists and by flags set by the programmer making the xxxget(2) call. It's up to the programmer to pass a key value as one of the arguments to the xxxget(2) system call. The key value provides a means by which different processes can access the IPC object they wish to share; callers using the same key value will have the same IPC identifier returned to them (assuming permissions allow). The following pseudocode illustrates how the process works.

```
ipcget(...,args...)
  if (key == IPC_PRIVATE)
    loop through each xxxid_ds structure
      if (allocated)
        continue through loop
      if (not allocated)
        init xxxid_ds structure and return
    reached end of loop and all are allocated, return ENOSPC
  else (key is not IPC_PRIVATE)
    loop through each xxxid_ds structure
      if (allocated)
        if (key matches key in ipc_perm structure)
          if (IPC_EXCL /* exclusive flag */)
            return error EEXIST
          if (access not allowed)
            return error EACCES
          else (it's allocated, key matches, not exclusive, access allowed)
        else /* it's allocated but key does not match *
          continue through loop
      else (not allocated)
        set pointer
        if (IPC_CREATE IS NOT SET)
          return error ENOENT /* there is no corresponding entry *
        if (end of loop, everything is allocated and no key match)
          return error ENOSPC
```

Summarizing the preceding pseudocode flow: a new xxxid_ds structure (where xxx is sem, shm, or msg) is initialized on behalf of the caller if there is a free slot and if there is no entry with a matching key, and if the caller specified IPC_CREATE or IPC_EXCL (or both). A pointer to an existing object is returned if the key does match and if the mode bits grant permission and it's not exclusive (i.e., it was not created with IPC_EXCL).

The ipcaccess() code is called at various points by the IPC support code in the kernel to verify permissions to the IPC resource requested. The code is straightforward: it verifies access permissions for the UID and GID of the caller against the mode bits in the ipc_perm structure. The initial mode of an IPC object is determined when the object is first created by an IPC get call, specified by the flag argument in the call, which represents access permission expressed in numeric form, similar to file access modes, as in:

```
shmget(key, size, IPC_CREATE | 0644);
```