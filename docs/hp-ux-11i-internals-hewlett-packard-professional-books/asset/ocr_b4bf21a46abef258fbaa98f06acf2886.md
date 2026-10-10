# Listing 8.10 q4> fields struct fileops

```
0 0 4 0 * fo_rw
4 0 4 0 * fo_ioctl
8 0 4 0 * fo_select
12 0 4 0 * fo_close
```

# The Buffer Cache

Just as the kernel keeps copies of open inode data in a cache, it also maintains a much larger cache of recently accessed file data blocks (or extents, depending on the type of file system). This buffer cache is a key component of the HP-UX operating system. Figure 8-17 provides an overview of the buffer cache design.

![](bbox=[0.15, 0.38, 0.85, 0.65])

A basic premise of the UNIX operating system is that every thing is a file. This model serves many purposes and greatly reduces the overall complexity of the operating system. With this in mind, it is understandable that everything that may be done to improve file performance provides a large payback.

# Being Flexible: The Dynamic Buffer Cache

The HP-UX implementation of a buffer cache follows a dynamic model. The buffer cache is mapped into the kernel's address space, but the physical pages allocated to it come from the same available memory pools as those used for user processes. In this manner, the buffer cache competes with user code for system memory resources.