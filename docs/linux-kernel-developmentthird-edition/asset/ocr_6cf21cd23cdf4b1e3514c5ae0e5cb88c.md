Here’s a description for each individual method:

+   void open(struct vm_area_struct *area)  
+   This function is invoked when the given memory area is added to an address space.

+   void close(struct vm_area_struct *area)  
+   This function is invoked when the given memory area is removed from an address space.

+   int fault(struct vm_area_struct *area, struct vm_fault *vmf)  
+   This function is invoked by the page fault handler when a page that is not present in physical memory is accessed.

+   int page_mkwrite(struct vm_area_struct *area, struct vm_fault *vmf)  
+   This function is invoked by the page fault handler when a page that was read-only is being made writable.

+   int access(struct vm_area_struct *vma, unsigned long address, void *buf, int len, int write)  
+   This function is invoked by `access_process_vm()` when `get_user_pages()` fails.

# Lists and Trees of Memory Areas

As discussed, memory areas are accessed via both the mmap and the mm_rb fields of the memory descriptor. These two data structures independently point to all the memory area objects associated with the memory descriptor. In fact, they both contain pointers to the same vm_area_struct structures, merely represented in different ways.

The first field, mmap, links together all the memory area objects in a singly linked list. Each vm_area_struct structure is linked into the list via its vm_next field. The areas are sorted by ascending address. The first memory area is the vm_area_struct structure to which mmap points. The last structure points to NULL.

The second field, mm_rb, links together all the memory area objects in a red-black tree. The root of the red-black tree is mm_rb, and each vm_area_struct structure in this address space is linked to the tree via its vm_rb field.

A red-black tree is a type of balanced binary tree. Each element in a red-black tree is called a node. The initial node is called the root of the tree. Most nodes have two children: a left child and a right child. Some nodes have only one child, and the final nodes, called leaves, have no children. For any node, the elements to the left are smaller in value, whereas the elements to the right are larger in value. Furthermore, each node is assigned a color (red or black, hence the name of this tree) according to two rules: The children of a red node are black, and every path through the tree from a node to a leaf must contain the same number of black nodes. The root node is always red. Searching of, insertion to, and deletion from the tree is an O(log(n)) operation.

The linked list is used when every node needs to be traversed. The red-black tree is used when locating a specific memory area in the address space. In this manner, the ker-