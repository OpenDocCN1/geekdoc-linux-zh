ment. The structure for each slot in a `seg_map` segment is defined in the `<vm/segmap.h>` header file, shown below.

```
/*
 * Each smap struct represents a MAXBSIZE-sized mapping to the
 * <sm_vp, sm_off> given in the structure. The location of
 * the structure in the array gives the virtual address of the
 * mapping. Structure rearranged for 64-bit sm_off.
 */
struct smap {
        struct vnode   *sm_vp;       /* vnode pointer (if mapped) */

        /*
         * These next 3 entries are coded as
         * ushort_t's if we wish to cache or remove.
         */
        struct smap    *sm_hash;     /* hash pointer */
        struct smap    *sm_next;     /* next pointer */
        struct smap    *sm_prev;     /* previous pointer */
        u_offset_t     sm_off;       /* file offset for mapping */

        ushort_t       sm_bitmap;    /* bitmap for locked translations */
        ushort_t       sm_refcnt;    /* reference count for uses */
};

struct smfree {
        struct smap    *sm_free;     /* free list array pointer */
                struct smap *sm_mtx; /* protects smap data of this color */
        kcondvar_t     sm_free_cv;
        ushort_t       sm_want;      /* someone wants a slot of this color */
};
```

**Header File** `<vm/seg_map.h>`

The smap structures are:

+   - **sm_vp** — The file (vnode) this slot represents (if slot not empty)
+   - **sm_hash, sm_next, sm_prev** — Hash list reference pointers
+   - **sm_off** — The file (vnode) offset for a block-sized chunk in this slot in the file
+   - **sm_bitmap** — Bitmap to maintain translation locking
+   - **sm_refcnt** — The number of references to this mapping caused by concurrent reads

The important fields in the smap structure are the file and offset fields, `sm_vp` and `sm_off`. These fields identify which page of a file is represented by each slot in the segment.