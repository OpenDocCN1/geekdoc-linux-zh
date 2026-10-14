```
module_put(THIS_MODULE);

return SUCCESS;
}
/**
 * Called when a process, which already opened the dev file, attempts to
 * read from it.
 */
static ssize_t device_read(struct file *filp, /* see include/linux/fs.h */
			    char __user *buffer, /* buffer to fill with data */
			    size_t length, /* length of the buffer */
			    loff_t *offset)
{
	/* Number of the bytes actually written to the buffer */
	int bytes_read = 0;
	const char *msg_ptr = msg;

	if ((*msg_ptr + *offset) { /* We are at the end of the message */
		*offset = 0; /* reset the offset */
		return 0; /* signify end of file */
	}

	msg_ptr += *offset;

	/* Actually put the data into the buffer */
	while (length && *msg_ptr) {
		/* The buffer is in the user data segment, not the kernel
		 * segment so "*" assignment won't work. We have to use
		 * put_user which copies data from the kernel data segment to
		 * the user data segment.
		 */
		put_user(*(msg_ptr++), buffer++);
		length--;
		bytes_read++;
	}

	*offset += bytes_read;

	/* Most read functions return the number of bytes put into the buffer. */
	return bytes_read;
}
/* Called when a process writes to dev file; echo "enable" > /dev/key_state */
static ssize_t device_write(struct file *filp, const char __user *buffer,
			    size_t length, loff_t *offset)
{
	char command[10];

	if (length > 10) {
		pr_err("command exceeded 10 char\n");
		return -EINVAL;
	}

	if (copy_from_user(command, buffer, length))
		return -EFAULT;
```