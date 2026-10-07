
```c
#include <sys/types.h>
#include <sys/fcntl.h>
#include <procfs.h>

typedef struct {
    long cmd;
    prwatch_t prwatch;
} ctl_t;

int main(int argc, char **argv) {
    int ctlfd;
    ctl_t ctl;
    int test;

    if ((ctlfd = open("/proc/self/ctl1", O_WRONLY)) < 0) {
        perror("/open/proc");
        exit(1);
    }

    ctl.cmd = PCOWATCH;
    ctl.prwatch.pr_vaddr = (uintptr_t)test;
    ctl.prwatch.pr_size = sizeof(int);
    ctl.prwatch.pr_wflags = WA_READ|WA_WRITE;

    if (write(ctlfd, &ctl, sizeof(ctl)) != sizeof(ctl)) {
        perror("Set PCOWATCH");
        exit(1);
    }

    test = 0;
}
```

When we attempt to write to the integer test, we trigger a waypoint trap, by default, the process core dumps.

$./watchpoint
Trace/Breakpoint Trap(coredump)

The /proc process information file, prinfo, contains information pertinent to the watchpoint trap and can be read into a struct pr_info. In particular, the si_addr field contains the virtual address of the memory reference that triggered the watchpoint, and the si_code field contains one of TRAP_WATCH, TRAP_WWATCH, or TRAP_XWATCH, indicating read, write, or execute access, respectively. The si_trafter field is zero unless WA_TRAPAFTER is in effect for this watched area; nonzero indicates that the current instruction is not the instruction that incurred the watchpoint trap. The si_pc field contains the virtual address of the instruction that incurred the trap. Figure 5.16 illustrates watchpoint data structures.

## Global Page Management

| struct proc | struct as |
| :--- | :--- |
| p_as | a_segs |
| | a_size |
| | a_nsegs |
| | a_flags |
| | a_hat |
| | a_tail |
| | a_watchcp |

| 256-MB Kernel Context |
| :--- |
| Stack |
| Libraries |
| HEAP |
| Executable - DATA |
| Executable - TEXT |

```c
struct watched_page
wp_forw
wp_back
wp_vaddr
wp_prot
```

Figure 5.16 Watchpoint Data Structures

## 5.7 Global Page Management

Pages are the fundamental unit of physical memory in the Solaris memory management subsystem. In this section, we discuss how pages are structured, how they are located, and how free lists manage pools of pages within the system.

### 5.7.1 Pages—The Basic Unit of Solaris Memory

Physical memory is divided into pages. Every active (not free) page in the Solaris kernel is a mapping between a file (vnode) and memory; the page can be identified with a vnode pointer and the page size offset within vnode. A page's identity is its vnode/offset pair. The vnode/offset pair is the backing store for the page and represents the file and offset that the page is mapping.

The hardware address translation (HAT) and address space layers manage the mapping between a physical page and its virtual address space (more about “Hardware Address Translation Layer” on page 190). The key property of the vnode/offset pair is reusability; that is, we can reuse each physical page for another task by simply synchronizing its contents in RAM with its backing store (the vnode and offset) before the page is reused.

For example, we can reuse a page of heap memory from a process by simply copying the contents to its vnode and offset, which in this case will copy the contents to the swap device. The same mechanism is used for caching files, and we simply use the vnode/offset pair to reference the file that the page is caching. If we were to reuse a page of memory that was caching a regular file, then we simply synchronize the page with its backing store (if the page has been modified) or just reuse the page if it is not modified and does not need resyncing with its backing store.

| struct page | | backing store |
| :--- | :--- | :--- |
| p_vnode | struct vnode | |
| p_offset | | |
| p_hash | v_pages | |
| p_vpnext | | vnode offset |
| p_vprev | | Global Hash List |
| p_next | | |
| p_prev | | Vnode's Page List |
| p_lcknt | | Free list or I/O List |
| p_cowcnt | | |
| p_selock | | |

Figure 5.17 The Page Structure

### 5.7.2 The Page Hash List

The VM system hashes pages with identity (a valid vnode/offset pair) onto the global hash list so that they can be located by vnode and offset. Three page functions search the global page hash list: page_find(), page_lookup(), and page_lookup_nowait(). These functions take a vnode and offset as arguments and return a pointer to a page structure if needed.

The global hash list is an array of pointers to linked lists of pages. The functions use a hash to index into the page_hash array to locate the list of pages that contains the page with the matching vnode/offset pair. Figure 5.18 shows how the page_find() function indexes into the page_hash array to locate a page matching a given vnode/offset.

## Global Page Management

```c
page_find(vnode, offset) {
  index = PAGE_HASH_FUNC (vnode, offset)
  page = PAGE_HASH_SEARCH \
  (index, vnode, offset)
}
```

![](img/a86367b95bf21add858c99948ac951c6_214_0.png)

Figure 5.18 Locating Pages By Their Vnode/Offset Identity

page_find() locates the slot in the page_hash array containing a list of potential

- 1. It calculates the slot in the page_hash array containing a list of potential pages by using the PAGE_HASH_FUNC macro, shown below.

```c
#define PAGE_SIZE page_hashrz
#define PAGE_HASHAVELEN 4
#define PAGE_HASHVPSHIFT 6
#define PAGE_HASH_FUNC(vp, off) ((off >> PAGESHIFT + \
  ((uintptr_t) (vp) >> PAGE_HASHVPSHIFT)) & \
  (PAGE_HASH - 1))
```
Header File <page.h>

- 2. It uses the PAGE_HASH_SEARCH macro, shown, to create the list referenced by the slot for a page matching vnode/offset. The macro traverses the linked list of pages until it finds such a page.

```c
int PAGE_HASH_SEARCH(index, pp, vp, off) {
  for ((pp) = page_hash[index]; (pp); (pp)->p_hash) {
    if ((pp)->p_node == (vp) && (pp)->p_offset == (off)) \
      break;
  }
}
```
Header File <page.h>

### 5.7.3 MMU-Specific Page Structures

The defined page structure is the same across different platforms and contains no machine-specific structures. We do, need to keep machine-specific data about every page, for example, the HAT information that describes how the page is mapped. The kernel wraps the machine-independent page structure with a machine-specific page structure, struct pagemap. The contents of the machine-specific page are hidden from the generic kernel—only the HAT machine-specific layer can see or manipulate its contents. Figure 5.19 shows how each page is embedded in structpage.

| struct machpage | |
| :--- | :--- |
| struct page | |
| p_inode | | |
| p_offset | | |
| p_hash | | |
| p_vpnext | | |
| p_vprev | | |
| p_next | | |
| p_prev | | |
| p_locknt | | |
| p_cowcnt | | |
| p_selock | HAT information about this page's translation to physical memory |
| p_pag | | |
| p_mapping | Software copies of page reference and modified bits |
| p_agenum | | |
| p_nrm | | |
| p_color | | |
| p_index | | |
| p_share | | |

Figure 5.19 Machine-Specific Page Structures: sun4u Example
