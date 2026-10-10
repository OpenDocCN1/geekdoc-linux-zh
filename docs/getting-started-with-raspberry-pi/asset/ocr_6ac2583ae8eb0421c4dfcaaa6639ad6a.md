```
​/proc/bus/usb/004:
total 0
-rw-r--r-- 1 root root 43 Dec 2 12:44 001
→ UHCI : bus4
```

The usbfs files corresponding to plugged-in devices contain the associated USB device and configuration descriptors. In the preceding example, read /proc/bus/usb/003/003 to get descriptor information for the camera and /proc/bus/usb/001/007 for the descriptor associated with the hard disk. Managing usbfs files is not straightforward however, because the device filenames get reused after a device is plugged out. The solution is to use the libusb library, which uses usbfs under the hood. Using libusb instead of directly operating on usbfs has another benefit: Your driver is likely to work unchanged on other operating systems that support this library. If you don't find libusb bundled along with your distribution, download its sources from http://libusb.sourceforge.net/. The full list of USB access functions offered by this library is available under the doc/ directory of the libusb sources.

Listing 19.6 implements a skeletal user space driver for the digital camera using an oft-used libusb programming template. The camera's vendor ID (0x04b0) and device ID (0x0205) are obtained from the /proc/bus/usb/devices output shown previously.

# Listing 19.6. A Skeletal User Space USB Driver Using libusb

```
Code View:
#include <usb.h>

/* From the libusb package */
#define DIGICAM_VENDOR_ID 0x04b0 /* From /proc/bus/usb/devices */
#define DIGICAM_PRODUCT_ID 0x0205 /* From /proc/bus/usb/devices */
int main(int argc, char *argv[]) {
struct usb_dev_handle *mydevice_handle;
struct usb_bus *usb_bus;
struct usb_device *mydevice;

/* Initialize libusb */
usb_init();
usb_find_buses();
usb_find_devices();

/* Walk the bus */
for (usb_bus = usb_buses; usb_bus; usb_bus = usb_bus->next) {
for (mydevice = usb_bus->devices; mydevice;
mydevice = mydevice->next) {
if ((mydevice->descriptor.idVendor == DIGICAM_VENDOR_ID) &&
(mydevice->descriptor.idProduct == DIGICAM_PRODUCT_ID)) {

/* Open the device */
mydevice_handle = usb_open(mydevice);

/* Send commands to the camera. This is the heart of the
driver. Getting information about the USB control
messages to which your device responds is often a
challenge since many vendors do not readily divulge
hardware details */
usb_control_msg(mydevice_handle, ...);
/* ... */
```