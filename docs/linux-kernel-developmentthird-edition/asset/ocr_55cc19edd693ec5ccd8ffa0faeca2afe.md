```
unsigned short pig;  /* 2 bytes */
char fox;           /* 1 byte */
};
```

The structure is not laid out exactly like this in memory because the natural alignment of the structure's members is insufficient. Instead, the compiler creates the structure such that in memory, the struct resembles the following:

```
struct animal_struct {
char dog;            /* 1 byte */
u8 __pad0[3];       /* 3 bytes */
unsigned long cat;   /* 4 bytes */
unsigned short pig;  /* 2 bytes */
char fox;            /* 1 byte */
u8 __pad1;          /* 1 byte */
};
```

The padding variables exist to ensure proper natural alignment.The first padding provides a 3-byte waste-of-space to place cat on a 4-byte boundary. This automatically aligns the remaining types because they are all smaller than cat. The second and final padding is to pad the size of the struct. The extra byte ensures the structure is a multiple of 4, and thus each member of an array of this structure is naturally aligned.

Note that sizeof(animal_struct) returns 12 for either of these structures on most 32-bit machines. The C compiler automatically adds this padding to ensure proper alignment. You can often rearrange the order of members in a structure to obviate the need for padding. This gives you properly aligned data without the need for padding and therefore a smaller structure:

```
struct animal_struct {
unsigned long cat;   /* 4 bytes */
unsigned short pig;  /* 2 bytes */
char dog;            /* 1 byte */
char fox;            /* 1 byte */
};
```

This structure is only 8 bytes in size. It might not always be possible to rearrange structure definitions, however. For example, if this structure were specified as part of a standard or already used in existing code, its order is set in stone, although such requirements are less common in the kernel (which lacks a formal ABI than user-space. Often, you might want to use a specific order for other reasons—for example, to best lay out variables to optimize cache behavior. Note that ANSI C specifies that the compiler must never change the order of members in a structure—it is always up to you, the programmer.

> 4If the compiler could arbitrarily change the order of items in a structure, any existing code using the structure would break. In C, functions calculate the location of variables in a structure simply by adding offsets to the base address of the structure.