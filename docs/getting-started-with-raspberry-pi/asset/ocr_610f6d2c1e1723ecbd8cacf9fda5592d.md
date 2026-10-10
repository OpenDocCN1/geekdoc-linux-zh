```
114
return 0;
} else {
    outb(offset, addrports[bank]); /* Read a byte */
    data = inb(dataports[bank]);
}
return data;
```

```
/*
 * Write data to specified CMOS bank
 */
void
port_data_out(unsigned char offset, unsigned char data,
               int bank)
{
    if (unlikely(bank >= NUM_CMOS_BANKS)) {
        printk("Unknown CMOS Bank\n");
        return;
    } else {
        outb(offset, addrports[bank]); /* Output a byte */
        outb(data, dataports[bank]);
    }
    return;
}
```

If a char driver's `write()` method returns successfully, it implies that the driver has assumed responsibility for the data passed down to it by the application. However it does not guarantee that the data has been successfully written to the device. If an application needs this assurance, it can invoke the `fsync()` system call. The corresponding `fsync()` driver method ensures that application data is flushed from driver buffers and written to the device. The CMOS driver does not need an `fsync()` method because, in this case, driver-writes are synonymous with device-writes.

If a user application has data sitting on multiple buffers that it needs to send to a device, it can request multiple driver writes, but that is inefficient for the following reasons:

+   1. The overhead of multiple system calls and related context switches.
+   2. The driver is the one who knows the device intimately, so it can probably do a more clever job of efficiently gathering data from different buffers and dispatching it to the device.

Because of this, vectored versions of `read()` and `write()` are supported on Linux and other UNIX flavors. The Linux char driver infrastructure used to offer two dedicated methods to perform vector operations: `readv()` and `writev()`. Starting with the 2.6.19 kernel release, these two methods have been folded into the generic *Linux Asynchronous I/O* (AIO) layer, however. Linux AIO is a broad topic and is outside the scope of this discussion, so we just concentrate on the synchronous vector capabilities offered by AIO.

The prototypes of the vector driver methods are as follows: