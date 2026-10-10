Look at `cmos_release()` (and the rest of the methods) to see how `private_data` is used to directly obtain a handle on the `cmos_dev` structure belonging to the corresponding CMOS bank.

# **Listing 5.2. Open and Release**

```
Code View:
```
/*
 * Open CMOS bank
 */
int
cmos_open(struct inode *inode, struct file *file)
{
 struct cmos_dev *cmos_devp;

/* Get the per-device structure that contains this cdev */
cmos_devp = container_of(inode->i_cdev, struct cmos_dev, cdev);

/* Easy access to cmos_devp from rest of the entry points */
file->private_data = cmos_devp;

/* Initialize some fields */
cmos_devp->size = CMOS_BANK_SIZE;
cmos_devp->current_pointer = 0;

return 0;
}

/*
 * Release CMOS bank
 */
int
cmos_release(struct inode *inode, struct file *file)
{
 struct cmos_dev *cmos_devp = file->private_data;

/* Reset file pointer */
cmos_devp->current_pointer = 0;

return 0;
}
```
```

# **Exchanging Data**

`read()` and `write()` are the basic char driver methods responsible for exchanging data between user space and the device. The extended `read()`/`write()` family contains several other methods, too: `fsync()`, `aio_read()`, `aio_write()`, and `mmap()`.

The CMOS driver operates on a simple memory device and does not have to work through some of the complexities faced by usual char drivers:

+   - CMOS data access routines do not need to sleep-wait for device I/O to complete, whereas `read()` and `write()` methods belonging to many char drivers have to support both blocking and nonblocking modes of operation. Unless a device file is opened in the nonblocking (`O_NONBLOCK`) mode, `read()` and `write()` are allowed to put the calling process to sleep until the corresponding operation completes.