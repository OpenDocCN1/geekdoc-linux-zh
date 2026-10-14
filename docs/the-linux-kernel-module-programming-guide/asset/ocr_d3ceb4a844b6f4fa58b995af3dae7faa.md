```
92  *offset += bytes_read;
93
94  /* Read functions are supposed to return the number of bytes actually
95   * inserted into the buffer.
96   */
97  return bytes_read;
98 }
99
100 /* called when somebody tries to write into our device file. */
101 static ssize_t device_write(struct file *file, const char __user *buffer,
102                             size_t length, loff_t *offset)
103 {
104     int i;
105
106     pr_info("device_write(%p,%p,%ld)", file, buffer, length);
107
108     for (i = 0; i < length && i < BUF_LEN; i++)
109         get_user(message[i], buffer + i);
110
111     /* Again, return the number of input characters used. */
112     return i;
113 }
114
115 /* This function is called whenever a process tries to do an ioctl on our
116  * device file. We get two extra parameters (additional to the inode and file
117  * structures, which all device functions get): the number of the ioctl
118  * called
119  * and the parameter given to the ioctl function.
120  *
121  * If the ioctl is write or read/write (meaning output is returned to the
122  * calling process), the ioctl call returns the output of this function.
123  */
124 static long
125 device_ioctl(struct file *file, /* ditto */
126              unsigned int ioctl_num, /* number and param for ioctl */
127              unsigned long ioctl_param)
128 {
129     int i;
130     long ret = SUCCESS;
131
132     /* We don't want to talk to two processes at the same time. */
133     if (atomic_cmpxchg(&already_open, CDEV_NOT_USED, CDEV_EXCLUSIVE_OPEN))
134         return -EBUSY;
135
136     /* Switch according to the ioctl called */
137     switch (ioctl_num) {
138     case IOCTL_SET_MSG:
139         /* Receive a pointer to a message (in user space) and set that to
140          * be the device's message. Get the parameter given to ioctl by
141          * the process.
142          */
143         char __user *tmp = (char __user *)ioctl_param;
144         char ch;
145
146         /* Find the length of the message */
147         get_user(ch, tmp);
148         for (i = 0; ch && i < BUF_LEN; i++, tmp++)
```