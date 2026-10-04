```
TRACE_CHR("\r")
}

TRACE_CHR("\n")

/* 5 */
kfree_s(ptr, sizeof(struct tdd_buf));
return i;
}
```

Once again, the buffer and count parameters into tdd_read() are a pointer to a buffer in user space and a character count which were passed as parameters into the associated read() system call, the obvious difference between this and the tdd_write() function being that this time the buffer is to receive characters from a message structure in the device driver. The numbered comments are:

+   1. Only read()s from /dev/tddr are permitted.
2. If there are no messages in the queue then the read() call will not block, but will return the value -1 with the variable errno set to the value ENODATA.
3. Unlink the head message from the queue and set the variable ptr to point to it.
4. Verify that the kernel can write to the specified memory block then copy either the number of characters asked for (count) or the actual number of characters in the message buffer (ptr->buf_size) whichever is the smaller, into the user space provided (buffer). It is the user's responsibility to ensure that the specified buffer is large enough to hold the requested number of characters – the kernel cannot do exhaustive checks.
5. Finally, free the old message structure back to the kernel and return the actual number of characters transferred.

# 26.7 ioctl Function

The ioctl() function for this driver is very simple but it does serve to illustrate the idea. Two new ioctl() calls are provided by this driver to switch the trace facilities on and off. This is done using the TDD_TRON and TDD_TROFF commands to ioctl() respectively:

```
static int tdd_ioctl(struct inode *inode, struct file *file,
unsigned int cmd, unsigned long arg)
{
    TRACE_TXT("tdd_ioctl")

    switch(cmd)
    {
```