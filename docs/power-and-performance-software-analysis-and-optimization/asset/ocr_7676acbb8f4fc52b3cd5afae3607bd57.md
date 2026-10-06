# CHAPTER 1 Early Intel® Architecture

To illustrate this concept, consider how to load the ith element of an array of integers foo[i]. Assume that the index, i, is stored in the ECX register, that the base address of foo[0] is stored in the EAX register, and the desired destination of the contents of foo[i] is the EBX register. Accessing foo[i] translates to the pointer arithmetic:

```
foo[i] = *(uintptr_t)foo + (i * sizeof(foo[0]))
```

Since each element foo[i] is an integer, sizeof(foo[0]) = 4, the ith element could be loaded into EBX with:

```
mov (%eax, %ecx), %ebx
```

The next element, i+1, could be loaded either by incrementing i or adding a displacement of:
mov 4(%eax,%ecx), %ebx

# 1.4.2 PAGING

Up to this point, memory address translations have occurred in one phase, logical, that a segmented address consisting of selector and an offset, to a physical address. The 80286 extended segmentation in order to accommodate the needs of rapidly advancing operating system. The design of the 80386 recognized that segmentation alone was not enough to meet these needs, and therefore paging was introduced.

With paging, memory address translations occur in two separate phases. In the first phase, the logical address is converted to a linear address, through the translation method for segmentation. In the second phase, the linear address, produced in the first phase, is converted to a physical address, through the translation method for paging. Notice that paging doesn't replace segmentation, but was designed to complement it.

In a system that implements paging, the address space is divided into multiple pages. A page is a fixed-size chunk of memory, which may or not be present in memory. The available physical memory of the system is divided into page frames. A page frame is a memory region capable of holding a page in memory. As required, pages are swapped in and out of the physical page frames.

Mappings are created between the linear and physical address space through a hierarchical memory structure comprising of multiple tables, referred to as page tables. The tables are divided into multiple levels, with each level representing pages of a different size. Each entry in the page tables can either map a page of the current size, or reference another table, which can then map a page of a smaller size or reference another table, and so on.

In the classic x86 paging mode present in the 80386, the page tables are divided into two levels, the page directory and a set of page tables. Each entry in the page directory (PDE), can either map a 4-MB page or reference one of the second level page tables. Each entry in the page tables, known as a