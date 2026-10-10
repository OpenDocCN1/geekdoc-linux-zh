```
    } k1_un;
} knem_obj_hdr_t;
```

Note the additional object `size` field. This is used for xlarge objects. Xlarge objects are not cached—that is, when freed they don't go back on a free list, they just get released. For small and large objects, the size of the object is in the free list header. But for xlarge objects we have no free list, and therefore no free-list header, so we have to store the size here. Figure 13-4 shows the layout of objects and object headers in memory.

# Small Objects ( < 4 K )

![](bbox=[0.1, 0.28, 0.85, 0.42])

# Large Objects ( >= 4 K )

![](bbox=[0.15, 0.45, 0.75, 0.58])

Figure 13-4 Memory Arena Objects and Object Headers

This combination of objects and object headers gives us better performance and better control over memory than does the bucket allocator.

# Object Free Lists

For fixed-size objects' the arena maintains one free list per SPU. The `ka_objlist` entry in the `knem_arena` structure is a pointer to an array of `knem_flist_hdr` structures, one for each SPU. This header has a pointer to the first free object, `kfn_head`. In addition, it has fields used for managing the list, such as the object size, current page count, and a pointer back to the arena it belongs in. Figure 13-5 illustrates the free list for fixed-size objects.

The free lists for variable-sized objects are different. Free memory objects are handled similarly to the way they were with the bucket allocator, with a set of buckets pointing to lists of different sized objects. In this way, when a new object is needed, the allocator can go to the free list and get an object that is already the correct size. One difference between this scheme and the older bucket allocator is that the bucket sizes are different. Because of the extra overhead of the