# 11.1.1 Kernel File Structures

The Solaris kernel does not implement a system file table in the traditional sense. That is, the systemwide list of file structures is not maintained in an array or as a linked list. A kernel object cache segment is allocated to hold file structures, and they are simply allocated and linked to the process and vnode as files are created and opened.

We can see in Figure 11.1 that each process uses file descriptors to reference a file. The file descriptors ultimately link to the kernel file structure, defined as a `file_t` data type, shown below.

```
typedef struct file {
        kmutex_t                f_lock;        /* short-term lock */
        ushort_t                f_flag;
        ushort_t                f_pad;         /* Explicit pad to 4-byte boundary */
        struct vnode *f_vnode;                 /* pointer to vnode structure */
        offset_t                f_offset;      /* read/write character pointer */
        struct cred *f_cred;                    /* credentials of user who opened it */
        caddr_t                 f_audit_data;   /* file audit data */
        int                     f_count;       /* reference count */
} file_t;
```

**Header File** `<sys/file.h>`

The fields maintained in the file structure are, for the most part, self-explanatory. The `f_lock` kernel mutex lock protects the various structure members. These include the `f_count` reference count, which lists how many threads have the file opened, and the `f_flag` file flags, described in “File Open Modes and File Descriptor Flags” on page 495.

Solaris allocates file structures for opened files as needed, growing the open file count dynamically to meet the requirements of the system load. Therefore, the maximum number of files that can be opened systemwide at any time is limited by available kernel address space, and nothing more. The actual size to which the kernel can grow depends on the hardware architecture of the system and the Solaris version the system is running. The key point is that a fixed kernel limit on a maximum number of file structures does not exist.

The system initializes space for file structures during startup by calling `file_cache()`, a routine in the kernel memory allocator code that creates a kernel object cache. The initial allocation simply sets up the `file_cache` pointer with space for one file structure. However, the kernel will have allocated several file structures by the time the system has completed the boot process and is available for users, as all of the system processes that get started have some opened files. As files are opened/created, the system either reuses a freed cache object for the file