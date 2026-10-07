address and length of the mapping, then creates a seg_vn-specific data structure
within the segvn structure's s_data field. The seg_vn-specific data structure
holds all of the information the seg_vn_vn driver needs to handle the address map-
pings for the segment.

The seg_vn-specific data structure (struct segvn_data) contains pointers to
t vnode that is mapped and to any anonymous memory that has been allocated
for this segment. The file system does most of the work of mapped files once the
mapping is created. As a result, the seg_vn driver is fairly simple—most of the
seg_vn work is done during creation and deletion of the mapping.

The more complex part of the seg_vn driver implementation is its handling of
anonymous memory pages within the segment, which we discuss in the sections
that follow. When we create a file mapping, we put the vnode and offset of the file
mapped into the segvn_data structure members, shown below: Figure 5.10 illustrates the seg_vn
segment driver relationship.

```
struct segvn_data {
  krlock_t lock;
  uchar_t prot;
  uchar_t maxprot;
  off_t offset;
  struct vnode *vnode;
  ulong_t anon_index;
  struct anon_map *map;
  struct vpage *page;
  struct cred *cred;
  size_t swresv;
  uchar_t advice;
  uchar_t flags;
};\ /* protect segvn_data and vpage array * /
 * true if per page protections present */
 * current segment if pageprot = 0 */
 * maximum segment protections */
 * type of sharing done. */
 * offset of vnode for mapping */
 * vnode that segment mapping is to */
 * starting index into anon map array
 * pointer to anon share structure, if needed */
 * creation, if needed */
 * credentials */
 * swap space reserved for this segment */
 * madflags flags for segment */
 * true per page advice set */
 * flags from sys/mman.h *
 * # of pages LOCKED in segvn */
```

# Header File <vm/seg_vn.h>

At this point we create an actual virtual memory mapping by talking to the
hardware through address translation functions by using the
map() function. The hat_map() function is the central function for creating
address space mappings. It calls into the hardware-specific memory implement-
tion for the platform to program the hardware MMU, so that memory address ref-
erences within the supplied address range will trigger the page fault handler in
t segment driver until a valid physical memory page has been placed at the