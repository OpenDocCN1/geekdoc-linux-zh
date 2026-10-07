```
/* The name for our device, as it will appear in
 * /proc/devices */
#define DEVICE_NAME"char_dev"
```

```
/* The maximum length of the message for the device */
#define BUF_LEN 80
```

```
/* Is the device open right now? Used to prevent
 * concurrent access into the same device */
static int Device_Open = 0;
```

```
/* The message the device will give when asked * */
static char Message[BUF_LEN];
```

```
/* How far did the process reading the message get?
 * Useful if the message is larger than the size of the
 * buffer we get to fill in device_read. */
static char *Message_Ptr;
```

```
/* This function is called whenever a process attempts
 * to open the device file */
static int device_open(struct inode inode,
		struct file *file)

{
#ifdef DEBUG
printk("device_open(%p)\n", file);
#endif
```

```
/* We don't want to talk to two processes at the
 * same time */
if (Device_Open)
	eturn -EBUSY;
```