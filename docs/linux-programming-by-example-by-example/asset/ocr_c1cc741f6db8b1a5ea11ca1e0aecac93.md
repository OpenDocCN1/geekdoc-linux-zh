# Using a Mapped File

Of course, it is one thing to map and unmap a file, but the whole idea is to *use* and manipulate the file. The calls discussed in this section—`msync`, `mprotect`, the `mlock` family, and `mremap`—enable you to do these things.

# Writing a Map to Disk

The `msync` function writes a mapped file to disk. It has the following prototype:

```
`int msync(const void *start, size_t length, int flags);`
```

`msync` flushes `length` bytes of the map to disk beginning at the memory address `start` address. The `flags` argument is a bitwise OR of one or more of the following:

+   * `MS_ASYNC`—Schedules a write and returns

+   * `MS_SYNC`—Writes data before `msync()` returns

+   * `MS_INVALIDATE`—Invalidates other maps of the same file so they will be updated with new data

# Changing Map Protections

The `mprotect` function modifies a memory map’s protection flags. It is prototyped as follows:

```
`int mprotect(const void *addr, size_t len, int prot);`
```

`mprotect` sets or changes the protections for the region that begins at `addr` to the protection level specified in `prot`. `prot` can be a bitwise OR of one or more of the flags listed in Table 8.1. It returns 0 on success. If it fails, `mprotect` returns −1 and sets `errno`.

# Locking Mapped Memory

*Memory locking* means preventing a memory area from being swapped to disk. In a multitasking, multiuser system such as Linux, areas of system memory (RAM) not in active use may temporarily be written to disk (swapped out) so that memory can be put to other uses. Locking the memory sets a flag that prevents it from being swapped out. There are four functions for locking and unlocking memory: `mlock`, `mlockall`, `munlock`, and `munlockall`. Their prototypes are listed here:

```
`int mlock(const void *addr, size_t len);`  
`int munlock(void *addr, size_t len);`  
`int mlockall(int flags);`  
`int munlockall(void);`
```