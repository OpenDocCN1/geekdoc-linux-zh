```
struct file_operations hello_fops = {
    owner: THIS_MODULE,
    read: hello_read,
    write: hello_write,
    ioctl: hello_ioctl,
    open: hello_open,
    release: hello_release,
};

module_init(hello_init);
module_exit(hello_exit);

MODULE_AUTHOR("Chris Hallinan");
MODULE_DESCRIPTION("Hello World Example");
MODULE_LICENSE("GPL");
```

This expanded device driver example includes many new lines. From the top, we've had to add a new kernel header file to get the definitions for the file system operations. We've also defined a major number for our device driver. (Note to device driver authors: This is not the proper way to allocate a device driver major number. Refer to the Linux kernel documentation (…/Documentation/devices.txt) or one of the excellent texts on device drivers for guidance on the allocation of major device numbers. For this simple example, we simply choose one that we know isn't in use on our system.)

Next we see definitions for four new functions, our open, close, read, and write methods. In keeping with good coding practices, we've adopted a consistent naming scheme that will not collide with any other subsystems in the kernel. Our new methods are called hello_open(), hello_release(), hello_read(), and hello_write(), respectively. For purposes of this simple exercise, they are do-nothing functions that simply print a message to the kernel log subsystem.

Notice that we've also added a new function call to our hello_init() routine. This line registers our device driver with the kernel. With that registration call, we pass a structure containing pointers to the required methods. The kernel uses this structure, of type struct file_operations, to bind our specific device functions with the appropriate requests from the file system. When an application opens a device represented by our device driver and requests a read() operation, the file system associates that generic read() request with our module's hello_read() function. The following sections examine this process in detail.