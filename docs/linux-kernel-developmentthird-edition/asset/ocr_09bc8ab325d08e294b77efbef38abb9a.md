identification number (UID) to a pointer. In addition to providing the three main map operations, Linux’s implementation also piggybacks an *allocate* operation on top of the *add* operation. This *allocate* operation not only adds a UID/value pair to the map but also generates the UID.

The idr data structure is used for mapping user-space UIDs, such as *inotify* watch descriptors or POSIX timer IDs, to their associated kernel data structure, such as the *inotify_watch* or *k_itimer* structures, respectively. Following the Linux kernel’s scheme of obfuscated, confusing names, this map is called *idr*.

# ## Initializing an idr

Setting up an idr is easy. First you statically define or dynamically allocate an idr structure. Then you call `idr_init()`: `void idr_init(struct idr *idp);`

For example:

```
struct idr id_huh; /* statically define idr structure */
idr_init(&id_huh); /* initialize provided idr structure */
```

# ## Allocating a New UID

Once you have an idr set up, you can allocate a new UID, which is a two-step process. First you tell the idr that you want to allocate a new UID, allowing it to resize the backing tree as necessary. Then, with a second call, you actually request the new UID. This complication exists to allow you to perform the initial resizing, which may require a memory allocation, without a lock. We discuss memory allocations in Chapter 12 and locking in Chapters 9 and 10. For now, let’s concentrate on using idr without concern to how we handle locking.

The first function, to resize the backing tree, is `idr_pre_get()`: `int idr_pre_get(struct idr *idp, gfp_t gfp_mask);`

This function will, if needed to fulfill a new UID allocation, resize the idr pointed at by *idp*. If a resize is needed, the memory allocation will use the *gfp_flags* *gfp_mask* (*gfp_flags* are discussed in Chapter 12). You do not need to synchronize concurrent access to this call. Inverted from nearly every other function in the kernel, `idr_pre_get()` returns one on success and zero on error—be careful!

The second function, to actually obtain a new UID and add it to the idr, is `idr_get_new()`: `int idr_get_new(struct idr *idp, void *ptr, int *id);`

This function uses the idr pointed at by *idp* to allocate a new UID and associate it with the pointer *ptr*. On success, the function returns zero and stores the new UID in *id*. On error, it returns a nonzero error code: -EAGAIN if you need to (again) call `idr_pre_get()` and -ENOSPC if the idr is full.