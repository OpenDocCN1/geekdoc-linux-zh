structures, which link to the kernel file structure. The file is abstracted in the kernel as a virtual file through the vnode, which links to the file-specific structures (based on the file type) through the v_data pointer in the vnode.

![](bbox=[0.176, 0.194, 0.901, 0.547])

The process-level uf_entry structures are allocated dynamically in groups of 24 as files are opened, up to the per-process open file limit. The uf_entry structure contains a pointer to the file structure (uf_ofile) and a uf_pop flag field used by the kernel to maintain file state information. The possible flags are FRESERVED, to indicate that the slot has been allocated, FCLOSING, to indicate that a file-close is in progress, and FCLOSEXEC, a user-settable close-on-exec flag, which instructs the kernel to close the file descriptor if an exec(2) call is executed. uf_entry also maintains a reference count in the uf_refcnt member. This count provides a means of tracking multiple references to the file in multithreaded processes.

The kernel establishes a default hard and soft limit for the number of files a process can have opened at any time. rlim_fd_max is the hard limit, and rlim_fd_cur is the current limit (or soft limit). A process can have up to rlim_fd_cur file descriptors and can increase the number up to rlim_fd_max. You can set these parameters systemwide by placing entries in the /etc/system file:

```
set rlim_fd_max=8192
set rlim_fd_cur=1024
```