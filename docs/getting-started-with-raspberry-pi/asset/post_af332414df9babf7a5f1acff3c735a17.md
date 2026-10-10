
## Device Example: Telemetry Card

Now that you know the basics of Linux-USB, it's time to look at an example device. Consider a system equipped with a telemetry card connected to the processor via internal USB, as shown in bus 2 of Figure 11.2. The card acquires data from a remote device and ferries it to the processor over USB. An example telemetry card is a medical-grade board that monitors or programs an implanted device.

Let's assume that our example telemetry card has the following endpoints having the semantics described in Table 11.2:

- A control endpoint attached to an on-card configuration register
- A bulk IN endpoint that passes remote telemetry information collected by the card to the processor
- A bulk OUT endpoint that transfers data in the reverse direction

### Table 11.2. Register Space in the Telemetry Card

| Register | Associated Endpoint |
| :--- | :--- |
| Telemetry Configuration Register | Control endpoint 0 (register offset 0x8). |
| Telemetry Data-In Register | Bulk IN endpoint. The endpoint address is assigned during device enumeration. |
| Telemetry Data-Out Register | Bulk OUT endpoint. The endpoint address is assigned during device enumeration. |

Let's build a minimal driver for this card partly based on the USB skeleton driver, `drivers/usb/usb-skeleton.c`.

Because PCMCIA, PCI, and USB devices have similar characteristics such as hotplug support, some driver methods and data structures belonging to these subsystems resemble each other. This is especially true for the portions responsible for initializing and probing. As we progress through the telemetry driver and notice parallels with what we learned for PCI drivers in Chapter 10, we will pause and take note.

### Initializing and Probing

Like PCI and PCMCIA drivers, USB drivers have `probe()`/`disconnect()` [2] methods to support hotplugging, and a table that contains the identity of devices they support. A USB device is identified by the `usb_device_id` structure defined in `include/linux/mod_devicetable.h`. You may recall from the previous chapter that the `pci_device_id` structure, also defined in the same header file, identifies PCI devices.

> [2] `disconnect()` is called `remove()` in PCI and PCMCIA parlance.

```c
struct usb_device_id {
    /* ... */
    __u16 idVendor;       /* Vendor ID */
    __u16 idProduct;      /* Device ID */
    /* ... */
    __u8  bDeviceClass;   /* Device class */
    __u8  bDeviceSubClass;/* Device subclass */
    __u8  bDeviceProtocol;/* Device protocol */
    /* ... */
};
```

`idVendor` and `idProduct`, respectively, hold the manufacturer ID and product ID, whereas `bDeviceClass`, `bDeviceSubClass`, and `bDeviceProtocol` categorize the device based on its functionality. This classification, determined by the USB specification, allows implementation of generic client drivers as discussed in the section “Class Drivers” later.

Listing 11.2 implements the telemetry driver’s initialization routine, `usb_tele_init()`, which calls on `usb_register()` to register its `usb_driver` structure with the USB core. As shown in the listing, `usb_driver` ties the driver’s `probe()` method, `disconnect()` method, and `usb_device_id` table together. `usb_driver` is similar to `pci_driver`, except that the `disconnect()` method in the former is named `remove()` in the latter.

### Listing 11.2. Initializing the Driver

```c
#define USB_TELE_VENDOR_ID  0xABCD  /* Manufacturer's Vendor ID */
#define USB_TELE_PRODUCT_ID 0xCDEF   /* Device's Product ID */

/* USB ID Table specifying the devices that this driver supports */
static struct usb_device_id tele_ids[] = {
  { USB_DEVICE(USB_TELE_VENDOR_ID, USB_TELE_PRODUCT_ID) },
  { } /* Terminate */
};

MODULE_DEVICE_TABLE(usb, tele_ids);

/* The usb_driver structure for this driver */
static struct usb_driver tele_driver = {
  .name       = "tele",              /* Unique name */
  .probe      = tele_probe,          /* See Listing 11.3 */
  .disconnect = tele_disconnect,     /* See Listing 11.3 */
  .id_table   = tele_ids,           /* See above */
};

/* Module Initialization */
static int __init
usb_tele_init(void)
{
  /* Register with the USB core */
  result = usb_register(&tele_driver);

  /* ... */
  return 0;
}

/* Module Exit */
static void __exit
usb_tele_exit(void)
{
  /* Unregister from the USB core */
  usb_deregister(&tele_driver);
  return;
}

module_init(usb_tele_init);
module_exit(usb_tele_exit);
```

The `USB_DEVICE()` macro creates a `usb_device_id` from the vendor and product IDs supplied to it. This is analogous to the `PCI_DEVICE()` macro discussed in the previous chapter. The `MODULE_DEVICE_TABLE()` macro marks `tele_ids` in the module image so that the module can be loaded on demand if the card is hotplugged. This is again similar to what we discussed for PCMCIA and PCI devices in the previous two chapters.

When the USB core detects a device with properties matching the ones declared in the `usb_device_id` table belonging to a client driver, it invokes the `probe()` method registered by that driver. When the device is unplugged or if the module is unloaded, the USB core invokes the driver's `disconnect()` method.

Listing 11.3 implements the `probe()` and `disconnect()` methods of the telemetry driver. It starts by defining a device-specific structure, `tele_device_t`, which contains the following fields:

- A pointer to the associated `usb_device`.
- A pointer to the `usb_interface`. Revisit Listing 11.1 to see this structure in use.
- A control URB (`ctrl_urb`) to communicate with the telemetry configuration register, and a `ctrl_req` to formulate programming requests to this register. These fields are described in the next section "Accessing Registers."
- The card has a bulk IN endpoint through which you can glean the collected telemetry information. Associated with this endpoint are three fields: `bulk_in_addr`, which holds the endpoint address; `bulk_in_buf`, which stores received data; and `bulk_in_len`, which contains the size of the receive data buffer.
- The card has a bulk OUT endpoint to facilitate downstream data transfer. `tele_device_t` has a field called `bulk_out_addr` to store the address of this endpoint. There are fewer data structures in the OUT direction because in this simple case we use a synchronous URB submission interface that hides several implementation details.

The kernel invokes the card's `probe()` method, `tele_probe()`, soon after enumeration. `tele_probe()` performs three tasks:

1. Allocates memory for the device-specific structure, `tele_device_t`.
2. Initializes the following fields in `tele_device_t` related to the device's bulk endpoints: `bulk_in_buf`, `bulk_in_len`, `bulk_in_addr`, and `bulk_out_addr`. For this, it uses the data collected by the hub driver during enumeration. This data is available in descriptor structures discussed in the section "Descriptor Structures."
3. Exports the character device `/dev/tele` to user space. Applications operate over `/dev/tele` to exchange data with the telemetry card. `tele_probe()` invokes `usb_register_dev()` and supplies it the `file_operations` that form the underlying pillars of the `/dev/tele` interface via the `usb_class_driver` structure.

The address of the device-specific structure allocated in Step 1 has to be saved so that other methods can access it. To achieve this, the telemetry driver uses a threefold strategy depending on the function arguments available to various driver routines. To save this structure pointer between the `probe()` and `open()` invocation threads, the driver uses the device's `driver_data` field via the pair of functions, `usb_set_intfdata()` and `usb_get_intfdata()`. To save the address of the structure pointer between the `open()` thread and other entry points, `open()` stores it in the `/dev/tele`'s `file->private_data` field. This is because the kernel supplies these char entry points with `/dev/tele`'s inode pointer as argument rather than the `usb_interface` pointer. To save the address of the device-specific structure from URB callback functions, the associated submission threads use the URB's context field as the storage area. Look at Listings 11.3, 11.4, and 11.5 to see these mechanisms in action.

All USB character devices answer to major number 180. If you enable `CONFIG_USB_DYNAMIC_MINORS` during kernel configuration, the USB core dynamically selects a minor number from the available pool. This behavior is similar to registering misc drivers after specifying `MISC_DYNAMIC_MINOR` in the `miscdevice` structure (as discussed in the section "Misc Drivers" in Chapter 5, "Character Drivers"). If you choose not to enable `CONFIG_USB_DYNAMIC_MINORS`, the USB subsystem selects an available minor number starting at the minor base set in the `usb_class_driver` structure.

### Listing 11.3. Probing and Disconnecting

```c
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
  /* ... */
};
```
