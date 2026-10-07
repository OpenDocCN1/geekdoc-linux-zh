```
printk ("device_release(%p,%p)\n", inode, file);
#endif
```

```
/* We're now ready for our next caller */
Device_Open --;
```

```
MOD_DEC_USE_COUNT;
```

```
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
return 0;
#endif
```

```
/* This function is called whenever a process which
* has already opened the device file attempts to
* read from it. */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static ssize_t device_read(
    struct file *file,
    char *buffer, /* The buffer to fill with the data */
    size_t length, /* The length of the buffer */
    loff_t *offset) /* offset to the file */
#else
static int device_read(
    struct inode *inode,
    struct file *file,
    char *buffer, /* The buffer to fill with the data */
    int length)
    /* The length of the buffer */
    * (mustn't write beyond!) */
#endif
```

```
{
    /* Number of bytes actually written to the buffer */
    int bytes_read = 0;
```