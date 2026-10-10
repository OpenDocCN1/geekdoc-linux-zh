
Bus=03 Lev=01 Prnt=01 Port=01 Cnt=01 Dev#= 5 Spd=12 MxCh= 0
Ver=1.10 Cls=00(>ifc) Sub=00 Prot=00 MxPS=64 #Cfgs= 1
Vendor=04b0 ProdID=0205 Rev=1.00
Manufacturer=Nikon
Product=Nikon Dsc E5200
SerialNumber=2507597
#Ifs= 1 Cfg#= 1 Atr=c0 MxPwr= 2mA
I: If#= 0 Alt= 0 #EPS= 2 Cls=08(stor.) Sub=06 Prot=50
 Driver=usb-storage
Ad=01(O) Attr=02(Bulk) MxPS= 64 Ivl=0ms
Ad=82(I) Attr=02(Bulk) MxPS= 64 Ivl=0ms

Bus=01 Lev=01 Prnt=01 Port=02 Cnt=01 Dev#= 12 Spd=480 MxCh= 0
Ver=2.00 Cls=00(>ifc) Sub=00 Prot=00 MxPS=64 #Cfgs= 1
Vendor=0bc2 ProdID=0501 Rev=0.01
Manufacturer=Seagate
Product=USB Mass Storage
SerialNumber=00000062459
#Ifs= 1 Cfg#= 1 Atr=e00 MxPwr=0mA
I: If#= 0 Alt= 0 #EPS= 2 Cls=08(stor.) Sub=06 Prot=50
 Driver=usb-storage
Ad=02(0) Attr=02(Bulk) MxPS= 512 Ivl=0ms
Ad=88(I) Attr=02(Bulk) MxPS= 512 Ivl=0ms

Look at the T: lines in the preceding output, which display the topology. As expected, the hard disk has arrived on the EHCI bus, bus1, and the camera has appeared on the UHCI bus, bus3. This is how the usbfs tree looks now:

# Code View:

```bash
ls -lR /proc/bus/usb
/proc/bus/usb:
total 0
dr-xr-xr-x 2 root root 0 Dec 2 12:44 001
dr-xr-xr-x 2 root root 0 Dec 2 12:44 002
dr-xr-xr-x 2 root root 0 Dec 2 12:44 003
dr-xr-xr-x 2 root root 0 Dec 2 12:44 004
-r--r----- 1 root root 0 Dec 2 19:51 devices

/proc/bus/usb/001:
total 0
-rw-r----- 1 root root 43 Dec 2 12:44 001
-rw-r----- 1 root root 50 Dec 2 19:51 007

/proc/bus/usb/002:
total 0
-rw-r----- 1 root root 43 Dec 2 12:44 001

/proc/bus/usb/003:
total 0
-rw-r----- 1 root root 43 Dec 2 12:44 001
-rw-r----- 1 root root 50 Dec 2 19:16 003

/proc/bus/usb/004:
total 0
-rw-r--r-- 1 root root 43 Dec 2 12:44 001
```

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_0.png)

EHCI: bus1

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_1.png)

High-speed disk

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_2.png)

UHCI: bus2

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_3.png)

UHCI: bus3

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_4.png)

Full-speed camera

The usbfs files corresponding to plugged-in devices contain the associated USB device and configuration descriptors. In the preceding example, read /proc/bus/usb/003/003 to get descriptor information for the camera and /proc/bus/usb/001/007 for the descriptor associated with the hard disk. Managing usbfs files is not straightforward however, because the device filenames get reused after a device is plugged out. The solution is to use the libusb library, which uses usbfs under the hood. Using libusb instead of directly operating on usbfs has another benefit: Your driver is likely to work unchanged on other operating systems that support this library. If you don't find libusb bundled along with your distribution, download its sources from http://libusb.sourceforge.net/. The full list of USB access functions offered by this library is available under the doc/ directory of the libusb sources.

Listing 19.6 implements a skeletal user space driver for the digital camera using an oft-used libusb programming template. The camera's vendor ID (0x04b0) and device ID (0x0205) are obtained from the /proc/bus/usb/devices output shown previously.

# Listing 19.6. A Skeletal User Space USB Driver Using libusb

```c
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

                /* Close the device */
                usb_close(mydevice_handle);
            }
        }
    }
}
```

# User Mode I²C

In Chapter 8, "The Inter-Integrated Circuit Protocol," you learned to develop kernel mode drivers for I²C devices; but sometimes, when you need to enable support for a large number of slow I²C devices, it makes sense to drive them from user space. The i2c-dev module enables the development of user mode I²C/SMBus device drivers. User-space code can access I²C host adapters via device nodes. To operate on the $n^{th}$ adapter, open /dev/i2c-n. After you have a file descriptor tied to a host adapter device node, you can command it through ioctls to connect to specific slave devices attached to it. You can then use the services of a family of data access routines to exchange data with the slaves.

Listing 19.7 is a simple user mode driver that performs common operations on an I²C EEPROM from user space. The EEPROM is the same as the one discussed in Chapter 8 and has two memory banks and a slave address corresponding to each bank. The listing uses inline functions from i2c-dev.h to operate on device nodes associated with the banks. Get this header file from the Im-sensors package (also discussed in Chapter 8) downloadable from www.im-sensors.org. This file contains user space equivalents for all kernel space I²C access functions listed in Table 8.1 of Chapter 8.

# Listing 19.7. A User Space I²C/SMBus Driver

```c
#include <linux/i2c.h>
#include <linux/i2c-dev.h>

/* Bus addresses of the memory banks */
#define SLAVE_ADDR1 0x60
#define SLAVE_ADDR2 0x61

int main(int argc, char *argv[])
{
    /* Open the host adapter */
    if ((smbus_fp = open("/dev/i2c-0", O_RDWR)) < 0) {
        exit(1);
    }

    /* Connect to the first bank */
    if (ioctl(smbus_fp, I2C_SLAVE, EEPROM_SLAVE_ADDR1) < 0) {
        exit(1);
    }

    /* ... */

    /* Dump data from the device */
    for (reg=0; reg < length; reg++) {
        /* See i2c-dev.h from the Im-sensors package for the
           implementation of the following inline function */
        res = i2c_smbus_read_byte_data(smbus_fp, (unsigned char) reg);
        if (res < 0) {
            exit(1);
        }

        /* Dump data */
        /* ... */
    }

    /* Switch to bank 2 */
    if (ioctl(smbus_fp, I2C_SLAVE, SLAVE_ADDR2) < 0) {
        exit(1);
    }

    /* Clear bank 2 */
    for (reg=0; reg < length; reg+=2){
        i2c_smbus_write_word_data(smbus_fp, (unsigned char) reg, 0x0);
    }

    /* ... */

    close(smbus_fp);
}
```

# UIO

Starting with the 2.6.23 release, the kernel includes a subsystem called UIO (*Userspace I/O*) that eases the implementation of some user-space drivers. UIO's intent is to allow the development of a bare-bones kernel driver for tasks such as interrupt handling, and push most of the device I/O logic to user space. UIO is especially relevant for some classes of industrial I/O cards.

Look inside *drivers/uio/* for the UIO sources. A user guide is available under *Documentation/DocBook/uio-howto.tmpl*. Exploring UIO is beyond the scope of this chapter.

# Looking at the Sources

The Linux scheduler lives in *kernel/sched.c*. The SCSI generic implementation is in *drivers/scsi/sg.c*, and *drivers/usb/core/devio.c* is responsible for supporting user space USB drivers. The i2c-dev driver that enables support for user mode I²C programming resides in *drivers/i2c/i2c-dev.c*.

Table 19.1 contains the main data structures used in this chapter, and Table 19.2 lists the functions that we used to aid user mode driver development.

**Table 19.1. Summary of Data Structures**

| Data Structure | Location (User Space) | Description |
|---|---|---|
| *sched_param* | */usr/include/bits/sched.h* | Information related to scheduling priorities. |
| *fb_var_screeninfo* | */usr/include/linux/fb.h* | Used to operate on frame buffers. Contains variable screen information such as resolution and pixelclock. See Chapter 11 for more details. |
| *sg_io_hdr_t* | */usr/include/scsi/sg.h* | Information to manage SCSI generic devices. |
| *usb_dev_handle* | Header files in the libusb package. | Structures to operate on USB devices from user space. |
| *usb_bus* | Header files in the libusb package. | Structures to operate on USB devices from user space. |

**Table 19.2. Summary of User-Space Functions**

| User-Space Function | Description |
|---|---|
| *sched_getparam()* | Obtains scheduling parameters associated with a given process |
| *sched_setscheduler()* | Sets scheduling parameters associated with a given process |
| *mlockall()* | Locks pages of the calling process in memory and thus avoids page faults |
| *ioperm()* | Controls access permissions to the first 0x3FF I/O ports |
| *iopl()* | Controls access privileges to all I/O ports |
| *outb() / outw() / outl()* | Outputs a byte/word/long to a specified port |
| *inb() / inw() / inl()* | Inputs a byte/word/long from a specified port |
| *mmap()* | Associates a file or a device address region with a chunk of user virtual memory |
| *msync()* | Flushes changes made to an mmap-ed memory area |
| *munmap()* | Reverse of mmap() |
| *usb_init()* | Functions provided by the libusb library to help you operate over usbfs |
| *usb_find_buses()* | Functions provided by the libusb library to help you operate over usbfs |
