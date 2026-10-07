endpoint VFS files have to be open for this transfer. The example demonstrates both methods for I/O transfers.

In a normal synchronous transfer, the threads use normal read and write operations. These operations are blocking calls in which the function has to wait until the transfer is complete.

```
status = read(sink_fd, buf, sizeof(buf);
status = write(source_fd, buf, len);
```

An asynchronous input/output (AIO) transfer is ideal for ISO transfers, enable you to submit one or more I/O requests in a system call without waiting for completion.

```
io_prep_write(iocb, source_fd,
buf, fill_in_buf(buf, iosize);
0);
io_set_callback(iocb, in_complete);
iocb->key = USB_DIR_IN;
```

```
status = io_submit(ctx, 1, &iocb)
if (status < 0) {
    perror(__FUNCTION__);
    break;
}
aio_in_pending++;
```

The AIO method of transfer helps you develop an application to stream data over gadgets. You can refer to the “More Reading” section to learn more about how program using the AIO infrastructure for Linux.

# SUMMARY

Developing drivers for the Linux kernel is more challenging and time consuming than developing drivers for user mode. User drivers satisfy the needs of protocols as USB. On Linux, libraries as libusb provide a generic driver infrastructure for USB devices that eliminates the need to develop device drivers in the kernel mode. Many USB applications on Linux have adopted libusb as their driver to reduce the developmental effort. Gadget functional drivers as Media Transfer Protocol (MTP) also operate from user mode. The gadgetfs framework makes it easy to write applications and reduces developmental efforts.