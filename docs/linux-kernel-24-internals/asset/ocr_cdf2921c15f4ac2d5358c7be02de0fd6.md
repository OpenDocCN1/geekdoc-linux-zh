```
```
module_init(init_pipe_fs)
module_exit(exit_pipe_fs)
```
```

The filesystem is of type `FS_NOMOUNT | FS_SINGLE`, which means it cannot be mounted from userspace and can only have one superblock system-wide. The `FS_SINGLE` file also means that it must be mounted via `kern_mount()` (after it is successfully registered via `register_filesystem()`, which is exactly what happens in `init_pipe_fs()`). The only bug in this function is that if `kern_mount()` fails (eg. because `kmalloc()` failed in `add_vfsmnt()`) then the filesystem is left as registered but module initialisation fails. This will cause **at /proc/filesystems** to fail. (have just sent a patch to Linus mentioning that although this is not a real bug today as pipes can’t be compiled as a module, it should be written with the view that in the future it may become modularised).

The result of `register_filesystem()` is that `pipe_fs_type` is linked into the `file_systems` list so one can read /proc/filesystems and find “pipel” entry in there with “nodev” flag indicating that `FS_REQUIRES_DEV` was not set. The /proc/filesystems file should really be enhanced to support all the new `FS_` flags (and I made a patch to do so) but it cannot be done because it will break all the user applications that use it. Despite Linux kernel interfaces changing every minute (only for the better) when it comes to the userspace compatibility, Linux is a very conservative operating system which allows many applications to be used for a long time without being recompiled.

The result of `kern_mount()` is that:

+   1. A new unnamed (anonymous) device number is allocated by setting a bit in `unnamed_dev_in_use` bitmap; if there are no more bits then `kern_mount()` fails with `EMFILE`.
+   2. A new superblock structure is allocated by means of `get_empty_super()`. The `get_empty_super()` function walks the list of superblocks headed by `super_block` and looks for empty entry, ie. `s->s_dev == 0`. If no such empty superblock is found then a new one is allocated using `kmalloc()` at `GFP_USER` priority. The maximum system-wide number of superblocks is checked in `get_empty_super()` so if it starts failing, one can adjust the tunable /proc/sys/fs/super-max.
+   3. A filesystem-specific `pipe_fs_type->read_super()` method, ie. `pipes_read_super()`, is invoked which allocates root inode and root dentry `sb->s_root`, and sets `sb->s_op` to be `pipefs_ops`.
+   4. Then `kern_mount()` calls `add_vfsmnt(NULL, sb->s_root, "none")` which allocates a new `vfsmnt` structure and links it into `vfsmnt_list` and `sb->s_mounts`.
+   5. The `pipe_fs_type->kern_mnt` is set to this new `vfsmount` structure and it is returned. The reason why the return value of `kern_mount()` is a `vfsmount` structure is because even `FS_SINGLE` filesystems can be mounted multiple times and their `mnt->mnt_sb` will point to the same thing which would be silly to return from multiple calls to `kern_mount()`.

Now that the filesystem is registered and in-kernel-mounted we can use it. The entry point into the pipes filesystem is the **pipe(2)** system call, implemented in arch-dependent function `sys_pipe()`, but the real work is done by a portable `fs/pipe.c:do_pipe()` function. Let us look at `do_pipe()` then. The interaction with pipes happens when `do_pipe()` calls `get_pipe_inode()` to allocate a new pipes inode. For this node, `inode->i_sb` is set to pipe's superblock `pipe_mnt->mnt_sb`, the file operations `i_fop` is set to `rdwr_pipe_fops` and the number of readers and writers (field in `inode->i_pipe`) is set to 1. The reason why there is a separate inode field `i_pipe` instead of keeping it in the `fs->private` union is that pipes and FIFOs share the same code and FIFOs can exist on other filesystems which use the other access paths within the same union which is very bad C and can work only by pure luck.

# 3.6 Example Virtual Filesystem: pipes