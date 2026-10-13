![](bbox=[0.151, 0.124, 0.899, 0.517])

# 5.7  Global Page Management

Pages are the fundamental unit of physical memory in the Solaris memory management subsystem. In this section, we discuss how pages are structured, how they are located, and how free lists manage pools of pages within the system.

# 5.7.1  Pages—The Basic Unit of Solaris Memory

Physical memory is divided into pages. Every active (not free) page in the Solaris kernel has a mapping between a file ( vnode) and memory; the page can be identified with a vnode pointer and the page sizeof offset within that vnode. A page’s identity is its vnode/offset pair. The vnode/offset pair is the backing store for the page and represents the file and offset that the page is mapping.

The hardware address translation (HAT) and address space layers manage the mapping between a physical page and its virtual address space (more about that in “The Hardware Address Translation Layer” on page 190). They keep property of the vnode/offset pair is reusability; that is, we can reuse each physical page for