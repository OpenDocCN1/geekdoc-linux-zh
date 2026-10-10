Table 13-1 The kmem_arena_attr Structure (Continued)
| Type | Name | Description |
| long | kat_minfent | Minimum number of objects to be kept on the free lists. |
| long | kat_maxpgcnt | Maximum number of pages in the arena for variable-sized objects. |
| long | kat_refillcnt | Minimum number of objects to be created at each refill. |
| kat_flags_t | kat_flags | Attribute flags. |
| size_t | kat_align | Alignment requirements for objects. |

# Objects and Object Headers

As mentioned, each object has an object header associated with it. When an object is on the free list, this header has a pointer to the next object on the list. When objects are in use, the header points back to the free list header in the arena it came from. Headers are stored differently depending on the size of the object.

For small objects, the header is stored immediately before the object in memory. The header in this case needs only a single pointer—the one that points to the free list if free or to the free list head if in use. We don’t need a pointer to the object itself because we know it immediately follows the header. The small object header looks like this:

```
```
typedef union kmem_obj_hdr {
  union kmem_obj_hdr *ko_fnext; /* Next element in free list */
  struct kmem_flist_hdr *ko_fhdr; /* Ptr to Free list header */
} kmem_obj_hdr_t;
```
```

For large objects, we have a global two-level structure for pointers to the object headers. The top level, kmem_lobj_hdr_tbl, is allocated at system initialization time. It is an array of pointers to second-level tables, which in turn are arrays of pointers to objects. To find a particular object header, the system uses the upper bits of the virtual page number to find the right entry in the first-level table, then follows that pointer and uses the lower bits of the virtual page number to find the second-level table entry. This is the object header.

Because the object headers for large objects are not next to the object itself, we need another field in the header. In addition to the pointer to the free list, we need a pointer to the object itself. The large object header builds on the small object header but adds this extra pointer:

```
```
typedef struct kmem_lobj_hdr {
  union kmem_obj_hdr kl_ohdr; /* Object header for large objects */
  union {
    void *kl_vaddr; /* Virtual address of object. */
    size_t kl_objsize; /* Object size */
  };
} kmem_lobj_hdr_t;
```
```