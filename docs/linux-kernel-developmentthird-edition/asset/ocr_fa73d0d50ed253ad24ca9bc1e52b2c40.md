+   * int open(struct inode *inode,
+           struct file *file)
+   Creates a new file object and links it to the corresponding inode object. It is called by the `open()` system call.

+   * int flush(struct file *file)
+   Called by the VFS whenever the reference count of an open file decreases. Its purpose is filesystem-dependent.

+   * int release(struct inode *inode,
+           struct file *file)
+   Called by the VFS when the last remaining reference to the file is destroyed—for example, when the last process sharing a file descriptor calls `close()` or exits. Its purpose is filesystem-dependent.

+   * int fsync(struct file *file,
+           struct dentry *dentry,
+           int datasync)
+   Called by the `fsync()` system call to write all cached data for the file to disk.

+   * int aio_fsync(struct kiocb *iocb,
+           int datasync)
+   Called by the `aio_fsync()` system call to write all cached data for the file associated with iocb to disk.

+   * int fasync(int fd, struct file *file, int on)
+   Enables or disables signal notification of asynchronous I/O.

+   * int lock(struct file *file, int cmd,
+           struct file_lock *lock)
+   Manipulates a file lock on the given file.

+   * ssize_t read(struct file *file,
+           const struct iovec *vector,
+           unsigned long count,
+           loff_t *offset)
+   Called by the `read()` system call to read from the given file and put the results into the count buffers described by vector. The file offset is then incremented.

+   * ssize_t write(struct file *file,
+           const struct iovec *vector,
+           unsigned long count,
+           loff_t *offset)
+   Called by the `write()` system call to write from the count buffers described by vector into the file specified by file. The file offset is then incremented.

+   * ssize_t sendfile(struct file *file,
+           loff_t *offset,