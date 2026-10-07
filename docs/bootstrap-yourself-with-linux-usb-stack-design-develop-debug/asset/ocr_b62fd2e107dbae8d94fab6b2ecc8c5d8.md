# More Reading

You can adopt options such as the UIO for the validation, which can provide a more stable, more flexible, and faster developmental setup than a kernel mode setup.

# MORE READING

You can explore more about the internals of libusb by downloading the source from http://www.libusb.org/. There are two versions of libusb: the legacy version (http://libusb.sourceforge.net/) and the libusb-1.0 version (http://libusb.sourceforge.net/api-1.0/). The newer version supports additional features such as isochronous transfer and asynchronous transfer. Over the years, many applications have adopted the legacy version. You can explore applications such as libptp (http://libptp.sourceforge.net/) and libmtp (http://libmtp.sourceforge.net/) to learn more about how functional drivers are developed based on libusb. The article found at http://blog.kernellkahani.com/?p=19 guides you to connect your MTP device on a Linux system. You can refer to http://www.linux-usb.org/gadget/ for a deeper understanding of gadgetfs. The site http://www.linux-usb.org/gadget.c provides a simple application using gadgetfs.

You can further explore space I/O from http://lwn.net/Articles/232575/ and http://www.osadl.org/UIO.uio.0.html. The http://lse.sourceforge.net/io/aio.html link provides further insights on the AIO infrastructure.