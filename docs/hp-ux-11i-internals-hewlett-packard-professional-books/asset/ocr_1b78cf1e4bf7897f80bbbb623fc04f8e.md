# **Listing 7.4** q4> fields fsdev_t

Pointer to next file system swap area with the same priority

```
0 0   4 0 *     fsw_next
```

The status flags

```
4 0   4 0 int   fsw_flags
```

Number of free swap pages

```
8 0   4 0 int   fsw_nfpgs
```

Number of blocks allocated

```
12 0  4 0 long  fsw_allocated
```

Minimum number of preallocated blocks

```
16 0  4 0 u.long fsw_min
```

The block allocation limit

```
20 0  4 0 u.long fsw_limit
```

The block reservation limit (File System swap equivalent to minimum free space)

```
24 0  4 0 u.long fsw_reserve
```

Priority for this file system swap space

```
28 0  4 0 int   fsw_priority
```

Pointer to the vnode for the file system's mount point

```
32 0  4 0 *     fsw_vnode
```

The underlying file system's block size

```
36 0  4 0 u.int fsw_bsize
```

This swap space's first swap table entry

```
40 0  2 0 short fsw_head
```

This swap space's last swap table entry

```
42 0  2 0 short fsw_tail
```

The directory path name for the underlying file system's mount point

```
44 0 256 0 char[256] fsw_mntpoint
```

# **Listing 7.5** q4> fields swpt_t

Index to the first free swpmap array entry

```
0 0 2 0 short st_free
```

Index of next chunk for same device or file system swap area

```
2 0 2 0 short st_next
```

Status flags (ST_INDEL|ST_FREE|ST_INUSE)

```
4 0 4 0 int   st_flags
```

Pointer to swap device

```
8 0 4 0 *     st_dev
```

Pointer to swap file system

```
12 0 4 0 *    st_fsp
```

Device of file system chunk vnode

```
16 0 4 0 *    st_vnode
```

Number of free pages on the device

```
20 0 4 0 int   st_nfpgs
```

Pointer to a swap maps starting address