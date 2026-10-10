
usb_submit_urb (tele_device->ctrl_urb, GFP_ATOMIC);

/* Wait until the callback returns indicating that the telemetry
   configuration register has been successfully initialized */
wait_for_completion (&tele_config_done);

/* Release our reference to the URB */
usb_free_urb (urb);

kfree (tmp);

/* Save the device-specific object to the file's private_data
   so that you can directly retrieve it from other entry points
   such as tele_read() and tele_write() */
file->private_data = tele_device;

/* Return the URB transfer status */
return (tele_device->ctrl_urb->status);
}

/* Callback function */
static void
tele_ctrl_callback (struct urb *urb)
{
complete ((struct completion *) urb->context);
}

You can render `tele_open()` simpler using `usb_control_msg()`, a blocking version of `usb_submit_urb()` that internally hides synchronization and callback details for control URBs. We preferred the asynchronous approach for learning purposes.

## Data Transfer

Listing 11.5 implements the `read()` and `write()` entry points of the telemetry driver. These methods perform the real work when an application reads or writes to `/dev/tele`. `tele_read()` performs synchronous URB submission because the calling process wants to block until telemetry data is available. `tele_write()`, however, uses asynchronous submission and returns to the calling thread without waiting for a confirmation that the data accepted by the driver has been successfully transferred to the device.

Because asynchronous transfers go hand in hand with a callback routine, Listing 11.5 implements `tele_write_callback()`. This routine examines `urb->status` to decipher the submission status. It also frees the transfer buffer allocated by `tele_write()`.

## Listing 11.5. Data Exchange with the Telemetry Card

```c
/* Read entry point */
static ssize_t
tele_read (struct file *file, char *buffer,
size_t count, loff_t *ppos)
{
int retval, bytes_read;
tele_device_t *tele_device;

/* Get the address of tele_device */
tele_device = (tele_device_t *)file->private_data;
/* ... */

/* Synchronous read */
retval = usb_bulk_msg(tele_device->usbdev, /* usb_device */
usb_rcvbulkpipe(tele_device->usbdev, /* Pipe */
tele_device->bulk_in_addr), /* Read buffer */
min(tele_device->bulk_in_len, count), /* Bytes to read */
&bytes_read, /* Bytes read */
5000); /* Timeout in 5 sec */

/* Copy telemetry data to user space */
if (!retval) {
    if (copy_to_user(buffer, tele_device->bulk_in_buf, bytes_read)) {
        return -EFAULT;
    } else {
        return bytes_read;
    }
}
return retval;
}

/* Write entry point */
static ssize_t tele_write(struct file *file, const char *buffer,
size_t write_count, loff_t *ppos)
{
char *tele_buf = NULL;
struct urb *urb = NULL;
tele_device_t *tele_device;

/* Get the address of tele_device */
tele_device = (tele_device_t *)file->private_data;
/* ... */

/* Allocate a bulk URB */
urb = usb_alloc_urb(0, GFP_KERNEL);
if (!urb) {
    return -ENOMEM;
}

/* Allocate a DMA-consistent transfer buffer and copy in data from user space. On return, tele_buf contains the buffer’s CPU address, while urb->transfer_dma contains the DMA address */
tele_buf = usb_buffer_alloc(tele_device->usbdev, write_count, GFP_KERNEL, &urb->transfer_dma);
if (copy_from_user(tele_buf, buffer, write_count)) {
    usb_buffer_free(tele_device->usbdev, write_count, tele_buf, urb->transfer_dma);
    usb_free_urb(urb);
    return -EFAULT;
}

/* Populate bulk URB fields */
usb_fill_bulk_urb(urb, tele_device->usbdev,
    usb_sndbulkpipe(tele_device->usbdev,
    tele_device->bulk_out_addr),
    tele_buf, write_count, tele_write_callback,
    tele_device);

/* urb->transfer_dma is valid, so preferably utilize
 * that for data transfer */
urb->transfer_flags |= URB_NO_TRANSFER_DMA_MAP;

/* Submit URB asynchronously */
usb_submit_urb(urb, GFP_KERNEL);

/* Release URB reference */
usb_free_urb(urb);

return(write_count);
}

/* Write callback */
static void
tele_write_callback(struct urb *urb)
{
    tele_device_t *tele_device;
    /* Get the address of tele_device */
    tele_device = (tele_device_t *)urb->context;
    
    /* urb->status contains the submission status. It's 0 if
     * successful. Resubmit the URB in case of errors other than
     * -ENOENT, -ECONNRESET, and -ESHUTDOWN */
    /* ... */
    
    /* Free the transfer buffer. usb_buffer_free() is the
     * release-counterpart of usb_buffer_alloc() called
     * from tele_write() */
    usb_buffer_free(urb->dev, urb->transfer_buffer_length,
    urb->transfer_buffer, urb->transfer_dma);
}
```

## Class Drivers

The USB specification introduces the concept of device classes and describes the functionality of each class driver. Examples of standard device classes include mass storage, networking, hubs, serial converters, audio, video, imaging, modems, printers, and human interface devices (HIDs). Class drivers are generic and let you plug and play a wide array of cards without the need for developing and installing drivers for every single device. The Linux-USB subsystem includes support for major class drivers.

Each USB device has a class and a subclass code. The mass storage class (`0x08`), for example, supports subclasses such as compact disc (`0x02`), tape (`0x03`), and solid-state storage (`0x06`). As you saw previously, device drivers populate the `usb_device_id` structure with the classes and subclasses they support. You can glean a device's class and subclass information by looking at the `:*` lines in the `/proc/bus/usb/devices` output.

Let's take a look at some important class drivers.

### Mass Storage

In USB parlance, mass storage refers to USB hard disks, pen drives, CD-ROMs, floppy drives, and similar storage devices. USB mass storage devices adhere to the Small Computer System Interface (SCSI) protocol to communicate with host systems. Block access to USB storage devices is hence routed through the kernel's SCSI subsystem. Figure 11.4 provides you an overview of the interaction between USB storage and SCSI subsystems. As shown in the figure, the SCSI subsystem is architected into three layers:

- 1. Top-level drivers for devices such as disks (`sd.c`) and CD-ROMs (`sr.c`)
- 2. A middle-level layer that scans the bus, configures devices, and glues top-level drivers to low-level drivers
- 3. Low-level SCSI adapter drivers

**Figure 11.4. USB mass storage and SCSI.**

![](img/07cc6f9c8c74622020874f66bfb53dc4_315_0.png)

The mass storage driver registers itself as a virtual SCSI adapter. The virtual adapter communicates upstream via SCSI commands and downstream using URBs. A USB disk appears to higher layers as a SCSI device attached to this virtual adapter.

To better understand the interactions between the USB and SCSI layers, let's implement a modification to the USB mass storage driver. The *usbfs* node */proc/bus/usb/devices*, contains the properties and connection details of all USB devices attached to the system. The “T:” line in the */proc/bus/usb/devices* output, for example, contains the bus number, the device's depth from the root hub, operational speed, and so on. The “P:” line contains the vendor ID, product ID, and revision number of the device. All the information available in */proc/bus/usb/devices* is managed by the USB subsystem, but there is one piece missing that is under the jurisdiction of the SCSI subsystem. The */dev* node name associated with the USB storage device (*sd[a-z][1-9]* for disks and sr[0-9] for CD-ROMs) is not available in /proc/bus/usb/devices. To overcome this limitation, let's add an "N:" line that displays the /dev node name associated with the device. Listing 11.6 shows the necessary code changes in the form of a source patch to the 2.6.23.1 kernel tree.

### Listing 11.6. Adding a Disk's /dev Name to usbfs

```diff
Code View:
include/scsi/scsi_host.h:
struct Scsi_Host {
/* ... */
void *host_data;
+ char sname[8]; /* /dev node name for this disk */
/* ... */
};

drivers/usb/storage/usb.h:
struct us_data {
/* ... */
+ char magic[4];
};

include/linux/usb.h:
struct usb_interface {
/* ... */
+ void *private_data;
};

drivers/usb/storage/usb.c:
static int storage_probe(struct usb_interface *intf,
const struct usb_device_id *id)
{
/* ... */
memset(us, 0, sizeof(struct us_data));
+ intf->private_data = (void *) us;
+ strcpy(us->magic, "disk", 4);
mutex_init(& (us->dev_mutex));
/* ... */
}

drivers/scsi/sd.c:
static int sd_probe(struct device *dev)
{
/* ... */
add_disk(gd);
+ memset (sdp->host->sname,0, sizeof (sdp->host->sname)) ;
+ strcpy (sdp->host->sname, gd->disk_name, 3);
sdev_printk(KERN_NOTICE, sdp, "Attached scsi %sdisk %s\n", sdp->removable ? "Removable " : "", gd->disk_name);
/* ... */
}

drivers/scsi/sr.c:
static int sr_probe(struct device *dev)
(
```
