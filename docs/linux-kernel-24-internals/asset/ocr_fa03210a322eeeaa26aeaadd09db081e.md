+   * **name**: human readable name, appears in `/proc/filesystems` file and is used as a key to find a filesystem by its name; this same name is used for the filesystem type in **mount(2)**, and it should be unique; there can (obviously) be only one filesystem with a given name. For modules, name points to module's address spaces and not copied: this means **cat /proc/filesystems** can oops if the module was unloaded but filesystem is still registered.

+   * **fs_flags**: one or more (Ored) of the flags: **FS_REQUIRES_DEV** for filesystems that can only be mounted on a block device, **FS_SINGLE** for filesystems that can have only one superblock, **FS_NOMOUNT** for filesystems that cannot be mounted from userpace by means of **mount(2)** system call; they can however be mounted internally using `kern_mount()` interface, e.g. pipes.

+   * **read_super**: a pointer to the function that reads the super block during mount operation. This function is required; if it is not provided, mount operation (whether from userspace or kernel) will always fail except in **FS_SINGLE** case where it will Oops in `get_sb_single()`, trying to dereference a **NULL** pointer in `fs_type->kern_mnt->mnt_sb` with (`fs_type->kern_mnt = NULL`).

+   * **owner**: pointer to the module that implements this filesystem. If the filesystem is statically linked into the kernel then this is **NULL**. You don't need to set this manually as the macro **THIS_MODULE** does the right thing automatically.

+   * **kern_mnt**: for **FS_SINGLE** filesystems only. This is set by `kern_mount()` (TODO: `kern_mount()` should refuse to mount filesystems if **FS_SINGLE** is not set).

+   * **next**: linkage into singly-linked list headed by `file_systems` (see `fs/super.c`). The list is protected by the `file_systems_lock` read–write spinlock and functions `register/unregister_filesystem()` modify it by linking and unlinking the entry from the list.

The job of the `read_super()` function is to fill in the fields of the superblock, allocate root inode and initialise any fs–private information associated with this mounted instance of the filesystem. So, typically the `read_super()` would do:

+   1. Read the superblock from the device specified via `sb->s_dev` argument, using buffer cache `bread()` function. If it anticipates to read a few more subsequest metadata blocks immediately then it makes sense to use `breada()` to schedule reading extra blocks asynchronously.
+   2. Verify that superblock contains the valid magic number and overall "looks" sane.
+   3. Initialise `sb->s_op` to point to `struct super_block_operations` structure. This structure contains filesystem–specific functions implementing operations like "read inode", "delete inode", etc.
+   4. Allocate root inode and root dentry using `d_alloc_root()`.
+   5. If the filesystem is not mounted read–only then set `sb->s_dirty` to 1 and mark the buffer containing superblock dirty (TODO: why do we do this? I did it in BFS because MINIX did it...)

# 3.3 File Descriptor Management

Under Linux there are several levels of indirection between user file descriptor and the kernel inode structure. When a process makes **open(2)** system call, the kernel returns a small non–negative integer which can be used for subsequent I/O operations on this file. This integer is an index into an array of pointers to `struct file`. Each file structure points to a dentry via `file->f_dentry`. And each dentry points to an inode via `dentry->d_inode`.

Each task contains a field `task->files` which is a pointer to `struct files_struct` defined in `include/linux/sched.h`.