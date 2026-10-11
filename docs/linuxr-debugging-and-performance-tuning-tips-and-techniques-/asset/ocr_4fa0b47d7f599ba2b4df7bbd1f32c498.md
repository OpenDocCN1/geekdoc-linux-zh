While it’s possible for free() to hand released memory back to the system and shrink the process address space, this is almost never done. Instead, the released memory is kept available for allocation by the next call to malloc(), calloc(), or realloc(). It may be that released memory continues to reside in the process’s address space. Security-sensitive programs may choose to do this. For example,

See Section 15.5.2, “Memory Allocation Debuggers”, page 612, for discussion of a number of useful dynamic-memory debugging tools.

# 3.2.1.4 Changing Size: realloc()

Dynamic memory has a significant advantage over statically declared arrays, which is that it’s possible to use exactly as much memory as you need, and no more. It’s not necessary to declare a global, static, or automatic array of some fixed size and hope that it’s (a) big enough and (b) not too big. Instead, you can allocate exactly as much as you need, no more and no less.

Additionally, it’s possible to change the size of a dynamically allocated memory area. Although it’s possible to shrink a block of memory, more typically, the block is grown. Changing the size is handled with realloc(). Continuing with the coordinates example, typical code goes like this:

```
```c
int new_count;
size_t new_amount;
struct coord *newcoords;

/* set new_count, for example: */
new_count = count * 2;          /* double the storage */
new_amount = new_count * sizeof(struct coord);

newcoords = (struct coord *) realloc(coordinates, new_amount);
if (newcoords == NULL) {        /* report error, recover or give up */
}

coordinates = newcoords;
/* continue using coordinates ... */
```
```

As with malloc(), the steps are boilerplate in nature and are similar in concept:

+   1. Compute the new size to allocate, in bytes.

+   2. Call realloc() with the original pointer obtained from malloc() (or from calloc() or an earlier call to realloc()) and the new size.