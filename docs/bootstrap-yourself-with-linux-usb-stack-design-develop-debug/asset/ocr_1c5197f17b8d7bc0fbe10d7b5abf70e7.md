successful open call, you can read the file for the descriptors to ensure that you are connected to the right device and bind to the interface to begin interacting with the device.

The user space driver generally employs these BBB/DDD files to control the USB devices. The drivers use input/output controls (IOCTLs) defined in /linux/usbdevice_fs to control and interact with the USB devices. In the next chapter, you will study user space details in using these IOCTLs to drive the USB devices. The table that follows lists the IOCTLs and their functionalities supported by the usbfs file.

| IOCTL | Description |
| --- | --- |
| USBDEVFS_CONTROL | IOCTL to send USB control messages. The user argument to call this IOCTL should be of type struct usdevfs_ctrltransfer. |
| USBDEVFS_BULK | IOCTL to send USB bulk messages. The user argument to call this IOCTL should be of type struct usdevfs_bulktransfer. |
| USBDEVFS_RESETP | IOCTL to reset a particular endpoint. The user argument to call this IOCTL should be of type unsigned int indicating the endpoint. |
| USBDEVFS_SETINTERFACE | IOCTL to set a particular interface. The user argument to call this IOCTL should be of type struct usdevfs_setinterface. |
| USBDEVFS_SETCONFIGURATION | IOCTL to set a particular configuration. The user argument to call this IOCTL should be of type unsigned int indicating the configuration number. |
| USBDEVFS_GETDRIVER | IOCTL to get a driver installed for a particular interface. The user argument to call this IOCTL should be of type struct usdevfs_getdriver. |
| USBDEVFS_SUBMITURB | IOCTL to transfer Request Block (URB) messages. The user argument to call this IOCTL should be of type struct usdevfs_urb. |
| USBDEVFS_DISCARDURB | IOCTL to kill a URB message. There is no argument for this IOCTL. |
| USBDEVFS_REAPURB | IOCTL to reap a URB message as a blocking call. The user argument is of a void data type. |
| USBDEVFS_REAPURNDELAY | IOCTL to reap a URB message as an unblocking call. The user argument is of a void data type. |