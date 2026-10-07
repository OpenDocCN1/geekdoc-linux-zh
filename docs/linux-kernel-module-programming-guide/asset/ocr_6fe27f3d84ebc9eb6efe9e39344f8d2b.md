# # Chapter 3

# # The /proc File System

In Linux there is an additional mechanism for the kernel and kernel modules to send information to processes — the /proc file system. Originally designed to allow easy access to information about processes (hence the name), it is now used by every bit of the kernel which has something interesting to report, such as /proc/modules which has the list of modules and /proc/meminfo which has memory usage statistics.

The method to use the proc file system is very similar to the one used with device drivers — you create a structure with all the information needed for the /proc file, including pointers to any handler functions (in case there is only one, the one called when somebody attempts to read from the /proc file). Then, init_module registers the structure with the cleanup_module registers it.

The reason we use register_dynamic is because we don't want to determine the index-node used for our file but allow the kernel to determine it to prevent clashes. Normal file systems are located on a disk, rather than just in memory (which is where /proc is), and in that case the index-node is a pointer to a disk location where the file's index-node (inode for for) is located. The node contains information about the file, the file's permissions, with a pointer to the disk location or locations where the file's data can be found.

Because we don't get called when the file is opened or closed, there's no where for us to put MOD_INC_COUNT and MOD_DEC_COUNT in this module, and if the file is opened and the module is removed, there's no way to avoid the consequences. In the next chapter we'll see a harder implement, but more flexible, way of dealing with

> In version 2.0, in version 2.2 this is done for if we set the node to zero.