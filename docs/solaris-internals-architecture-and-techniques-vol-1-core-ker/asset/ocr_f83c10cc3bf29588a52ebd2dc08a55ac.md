structures, which link to the kernel file structure. The file is abstracted in the ker-nel as a virtual file through the vnode, which links to the file-specific structures (based on the file type) through the v_data pointer in the vnode.

![](bbox=[0.158, 0.183, 0.915, 0.483])

Process view of an opened file Virtual file abstraction

File 11.1 File-Related Structures

The process-level uf_entry structures are allocated dynamically in groups of 24 as files are opened, up to the per-process open file limit. The uf_entry structure contains a pointer to the file structure (uf_ofile) and a uf_profile file field used by the kernel to maintain file state information. The possible flags are FRE-SERVED, to indicate that the slot has been allocated, FCLOSING, to indicate that a file-close is in progress, and FCLOSEEXEC, a user-selectable close-on-exec flag, which instructs the kernel to close the file descriptor if an exec(2) call is executed. uf_entry also maintains a reference count in the uf_refcnt member. This count provides means of tracking multiple references to the file in multithreaded processes.

The kernel establishes a default hard and soft limit for the number of files a process can have opened at any time. rlim_fd_max is the hard limit, and rlim_fd_cur is the current limit (or soft limit). A process can have up to rlim_fd_cur file descriptors and can increase the number to rlim_fd_max. You can set these parameters systemwide by placing entries in the /etc/system file:

```
set rlim_fd_max=8192
set rlim_fd_cur=1024
```