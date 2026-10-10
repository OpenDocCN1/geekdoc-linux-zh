# 284

Chapter 11. Universal Serial Bus

```
```c
 /* ... */
 unsigned char *setup_packet; /* (in) setup packet */
 /* ... */
 int interval; /* (modify) transfer interval
                (INT/ISO) */
 /* ... */
 void *context; /* (in) context for completion */
 usb_complete_t complete; /* (in) completion routine */
 /* ... */
};
```
```

There are three steps to using a URB: create, populate, and submit. To create a URB, use `usb_alloc_urb()`. This function allocates and zeros-out URB memory, initializes a kobject associated with the URB, and initializes a spinlock to protect the URB.

To populate a URB, use the following helper routines offered by the USB core:

```
```c
 void usb_fill_[control|int|bulk]_urb(
     struct usb *urb,           /* URB pointer */
     struct usb_device *usb_dev, /* USB device structure */
     unsigned int pipe,         /* Pipe encoding */
     unsigned char *setup_packet, /* For Control URBs only! */
     void *transfer_buffer,     /* Buffer for I/O */
     int buffer_length,         /* I/O buffer length */
     usb_complete_t completion_fn, /* Callback routine */
     void *context,             /* For use by completion_fn */
     int interval);            /* For Interrupt URBs only! */
```
```

The semantics of the previous routines will get clearer when we develop the example driver later on. These helper routines are available to control, interrupt, and bulk URBs but not to isochronous ones.

To submit a URB for data transfer, use `usb_submit_urb()`. URB submission is asynchronous. The `usb_fill_[control|int|bulk]_urb()` functions listed previously take the address of a callback function as argument. The callback routine executes after the URB submission completes and accomplishes things such as checking submission status and freeing the data-transfer buffer.

The USB core also offers wrapper interfaces that provide a facade of synchronous URB submission:

```
```c
 int usb_[control|interrupt|bulk]_msg(struct usb_device *usb_dev,
     unsigned int pipe, ...);
```
```

`usb_bulk_msg()`, for example, builds a bulk URB, submits it, and blocks until the operation completes. You don't have to supply a callback function because a generic completion routine serves that purpose. You don't need to explicitly create and populate the URB either, because `usb_bulk_msg()` does that for you at no additional cost. We will use this interface in our example driver.

`usb_free_urb()` is used to free a reference to a completed URB, whereas `usb_unlink_urb()` cancels a pending URB operation.

As mentioned in the section "Sysfs, Kobjects, and Device Classes" in Chapter 4, "Laying the Groundwork," a URB contains a kref object to track references to it. `usb_submit_urb()` increments the reference count using `kref_get()`. `usb_free_urb()` decrements the reference count using `kref_put()` and performs the free