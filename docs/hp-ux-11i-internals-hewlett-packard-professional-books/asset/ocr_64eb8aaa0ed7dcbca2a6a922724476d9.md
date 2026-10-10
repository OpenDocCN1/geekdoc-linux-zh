+   fd_lock          a spinlock structure
+   *fd_file        a pointer to a system file table file entry
+   fd_locker_tid   a reference to a locking thread
+   fd_state        the current descriptor state
+   fd_file          reference to the ofile partition entry

The kernel file system table consists of nfile entries (kernel-tunable) of type file. See Listings 8.9 and 8.10.

# Listing 8.9 q4> fields struct file

The file descriptor table flags are:

```
0 0 4 0 int          f_flag
```

+   0x01FREAD          descriptor is readable
+   0x02FWRITE         descriptor is writable
+   0x04FNDELAY        no delay
+   0x08FAPPEND        append on each write

The kernel object represented by this entry

```
4 0 2 0 short        f_type
```

+   0x01DTYPE_VNODE      regular file
+   0x02DTYPE_SOCKET     Berkeley IPC Socket
+   0x03DTYPE_STREAMS    Streams ftype type
+   0x05DTYPE_UNSP       user msg control
+   0x06DTYPE_LLA        link-level LAN access

```
link count from the message queue
6 0 2 0 short        f_msgcount
reference count
8 0 4 0 int           f_count
type-specific file system operations array pointer
12 0 4 0 *            f_ops
pointer to this file\'s vnode/socket kernel data
16 0 4 0 *            f_data
20 0 4 0 int          f_freeindex
24 0 8 0 long long    f_offset
32 0 4 0 *            f_buf
```

```
credentials of user who opened the file
36 0 4 0 *            f_cred
```

```
kernel beta-semaphore
40 0 1 0 u_char       f_b_sema.b_lock
42 0 2 0 u_short      f_b_sema.order
44 0 4 0 *            f_b_sema.owner
data intercept audit flag
48 0 2 0 short        f_tap
```