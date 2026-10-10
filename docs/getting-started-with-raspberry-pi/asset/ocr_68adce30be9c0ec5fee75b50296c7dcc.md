+   1.  Allocates memory for the device-specific structure, `tele_device_t`.

+   2.  Initializes the following fields in `tele_device_t` related to the device's bulk endpoints: `bulk_in_buf`, `bulk_in_len`, `bulk_in_addr`, and `bulk_out_addr`. For this, it uses the data collected by the hub driver during enumeration. This data is available in descriptor structures discussed in the section "Descriptor Structures."

+   3.  Exports the character device `/dev/tele` to user space. Applications operate over `/dev/tele` to exchange data with the telemetry card. `tele_probe()` invokes `usb_register_dev()` and supplies it the `file_operations` that form the underlying pillars of the `/dev/tele` interface via the `usb_class_driver` structure.

The address of the device-specific structure allocated in Step 1 has to be saved so that other methods can access it. To achieve this, the telemetry driver uses a threefold strategy depending on the function arguments available to various driver routines. To save this structure pointer between the `probe()` and `open()` invocation threads, the driver uses the device's `driver_data` field via the pair of functions, `usb_set_intfdata()` and `usb_get_intfdata()`. To save the address of the structure pointer between the `open()` thread and other entry points, `open()` stores it in the `/dev/tele`'s file→`private_data` field. This is because the kernel supplies these char entry points with `/dev/tele`'s inode pointer as argument rather than the `usb_interface` pointer. To save the address of the device-specific structure from URB callback functions, the associated submission threads use the URB's context field as the storage area. Look at Listings 11.3, 11.4, and 11.5 to see these mechanisms in action.

All USB character devices answer to major number 180. If you enable `CONFIG_USB_DYNAMIC_MINORS` during kernel configuration, the USB core dynamically selects a minor number from the available pool. This behavior is similar to registering misc drivers after specifying `MISC_DYNAMIC_MINOR` in the `miscdevice` structure (as discussed in the section "Misc Drivers" in Chapter 5, "Character Drivers"). If you choose not to enable `CONFIG_USB_DYNAMIC_MINORS`, the USB subsystem selects an available minor number starting at the minor base set in the `usb_class_driver` structure.

# Listing 11.3. Probing and Disconnecting

```
Code View:
/* Device-specific structure */
typedef struct {
  struct usb_device      *usbdev;      /* Device representation */
  struct usb_interface   *interface;   /* Interface representation*/
  struct urb             *ctrl_urb;    /* Control URB for
                                         register access */
  struct usb_ctrlrequest ctrl_req;     /* Control request
                                         as per the spec */
  unsigned char          *bulk_in_buf; /* Receive data buffer */
  size_t                 bulk_in_len;  /* Receive buffer size */
  __u8                   bulk_in_addr; /* IN endpoint address */
  __u8                   bulk_out_addr; /* OUT endpoint address */
  /* ... */                   /* Locks, waitqueues,
                               statistics.. */
} tele_device_t;

#define TELE_MINOR_BASE 0xA8    /* Assigned by the Linux-USB
                                   subsystem maintainer */

/* Conventional char driver entry points.
   See Chapter 5, "Character Drivers." */
static struct file_operations tele_fops =
{
  .owner    = THIS_MODULE,  /* Owner */
```