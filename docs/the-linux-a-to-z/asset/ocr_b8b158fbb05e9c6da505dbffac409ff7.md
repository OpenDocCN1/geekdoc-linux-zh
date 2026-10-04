The main system calls for use with a character device or file are: open(), close(), read(), write() and ioctl(). Each of these system calls, when it has been established that they are intended for your driver, can result in the appropriate driver function being executed.

# 25.3.1 open Function

The driver's open() function is called when a user process executes an open() system call on a device special file associated with this driver. The open() function has the prototype:

```
int open(struct inode *inode, struct file *file);
```

where the inode parameter is a pointer to the inode structure of the device special file which was accessed, and file is a pointer to the file structure for this device.

Typical actions for the open() function are:

+   - Determine that the associated hardware (if any) is available and on-line.
- Verify that the minor device number in MINOR(inode->i_rdev) is valid (i.e. in the expected range).
- If only one process should be able to open the device at a time then open() should test and set a driver flag to busy the device, or return -EBUSY if the flag is already set.
- Return a negative value if any kind of error occurs.
- Return the value zero on success.

# 25.3.2 release Function

The driver's release() function is only called when the last user process which has the device open close()s it:

```
void release(struct inode *inode, struct file *file);
```

where inode is a pointer to the inode structure of the device special file, and file is a pointer to the file structure for this device.

The release() function may be required to:

+   - Perform cleanup actions if there is any unfinished I/O in progress.
- Release hardware resources if necessary.
- Reset any exclusive access flags set by open().