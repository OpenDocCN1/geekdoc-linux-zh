```
TRACE_TXT("tdd_write")

/* 1 */
if (MINOR(inode->i_rdev)!=TDD_WRITE)
    return -EINVAL;

/* 2 */
if ((ptr = kmalloc(sizeof(struct tdd_buf), GFP_KERNEL))==0)
    return -ENOMEM;

/* 3 */
len = count<MAX_BUF?count:MAX_BUF;

if (verify_area(VERIFY_READ, buffer, len))
    return -EFAULT;

for (i = 0; i<count && i<MAX_BUF; ++i)
{
    ptr->buffer[i] = get_user_byte(buffer+i);
    TRACE_CHR("w")
}

/* 4 */
ptr->link = 0;

if (qhead==0)
    qhead = ptr;
else
    qtail->link = ptr;

qtail = ptr;
TRACE_CHR("\n")

/* 5 */
ptr->buf_size = i;
return i;
}
```

The third and fourth parameters to tdd_write() are the buffer and character count passed by the user process into the write() system call. The contents of this buffer need to be copied into the device driver's internal linked list of messages. Remember, though, that you cannot access the user space memory directly via the buffer parameter to tdd_write(); you have to use one of the special data transfer functions for that job. The numbered comments in the listing are as follows:

+   1. Check and ensure that only the process with /dev/tddw open writes messages.