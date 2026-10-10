# # Pointers

Pointers are a powerful C concept used for creating complex data structures. They are also among the most misunderstood aspects of C.

Conceptually, all the memory in a computer is laid out as an array of bytes. (At least, this is how the C language views it. It may not reflect reality.) Under Linux, a process has a virtual address space of 32 bits. That is, the process "sees" memory as a huge array with $4294967296\ (2^{32})$ one-byte entries.

**Note**

This is not strictly true. Processes under Intel Linux have a 2GB virtual address space, and processes under Alpha Linux have around 8TB of virtual address space. But it's close enough for illustrative purposes.

Every data object in C is placed somewhere in memory. For example, if you declare an **int** variable, it might be placed in memory locations 19387576 through 19387579, assuming that it occupies 4 bytes of memory. In general, you have no control over where objects are placed; the linker and the operating system hand these details. You also almost never need to know the exact numerical value of an object's location in memory.

However, you can obtain the address of a variable at **runtime**. You can store this address in a pointer. At a later time, you can **dereference** the pointer to access the original memory locations. And that is all there is to pointers—nothing more.

To take the address of a variable, use the **&** operator. To dereference a pointer, use the **\*** unary operator. Here is an example:

```
```
int a = 10;
int *aPtr;

aPtr = &a;
```
```

Note how we declare a pointer: Use an asterisk just before the variable name in the declaration. The declaration of `aPtr` should be read: Declare `aPtr` as pointer to `int`.

The **assignment** assigns the address of a to `aPtr`. Now, the expressions a and `*aPtr`, which are both **lvalues**, refer to exactly the same object. For example, consider these statements:

```
```
int a = 10;
int b;
int *aPtr;
```
```