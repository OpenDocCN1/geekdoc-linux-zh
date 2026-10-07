Some key interface functions act like a HDI between the HCD and the usbcore framework along with the preceding callback functions.

+   - int usb_hcd_submit_urb(struct *urb, gfp_t mem_flags)

The transfer of USB data to and from the host is using the USB Request Block (URB) data structure. This acts as an interface for the usb_submit_urb method and provides access to the host controller through the usb_enqueue callback.

+   - int usb_hcd_unlink_urb(struct *urb, int status)

This interface function allows the usbcore to cancel a URB submission and unlink it from the URB queue. usb_unlink_urb invokes this function to abort and cancel URB submissions.

+   - void usb_hcd_giveback_urb(struct usb_hcd *hcd, struct *urb,int status);

This interface function returns the information collected for the URB request to the driver. This interface handles over the URB from the HCD to the device driver using the usb_hcd_giveback_urb function.

+   - struct usb_hcd *usb_create_hcd(const struct hc_driver *driver,struct device *dev, const char *busname)

This interface function allocates and initializes a struct usb_hcd data structure and returns NULL if memory is unavailable. The host drivers use this function on a successful probe to allocate a struct usb_hcd data structure.

+   - int usb_add_hcd(struct usb_hcd *hcd,unsigned int irqnum, unsigned int irqflags)

This interface function initializes struct usb_hcd with necessary resources such as memory and interrupts and registers the bus. The function calls the HCD's reset and start routines.

+   - void usb_remove_hcd(struct usb_hcd *hcd)

This interface function is invoked during the shutdown process. It releases resources allocated during the usb_add_hcd function and invokes the HCD driver’s stop function.